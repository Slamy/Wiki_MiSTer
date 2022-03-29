# Developer journey: Implementing the Head On sound PCB
This page contains a description of how we implemented the sound PCB of the game Head On from SEGA/Gremlin.

## First steps
We analyzed the schematics of the Head On sound PCB board. Identifying circuits for individual sounds, and repeated parts of the circuit.
![head-on audio board analysis](https://user-images.githubusercontent.com/727070/159781502-7407a16c-356e-4d6b-8e8b-e0f9c0b8f8aa.png)
We talked about what we thought is what, and decided to start with the car sound.

## Finding real footage
Searching the web for video's with the sounds, we found a couple, but the quality was bad:

* https://www.youtube.com/watch?v=7souF1hpxAg
* https://www.youtube.com/watch?v=kCkWxaUi1LU

JimmyStones contacted the maker of the sound board, to see if he had some tips. He seemed willing to help, but not familiar enough with the fpga domain to join the project.
Then JimmyStones found someone who owns a cabinet and was able to obtain some good sound recordings.

This gave us a way to validate our results.

## Simulating and analyzing
### Car
We started by implementing the car sound in the falstad simulator.
It took some tweaking, mostly getting things like the diode type and transistor beta values right.
We managed to get a result that sounded pretty much like the real deal.
This is the final circuit:
[car_circuit.txt](https://github.com/MiSTer-devel/Main_MiSTer/files/8336074/car_circuit.txt)
it can be loaded into the [falstad simulator](https://www.falstad.com/circuit/)
From there it is possible to record a wav file, which we used to analyze the sound.

It turns out that the car sound consists of a repeating waveform that looks like this:

![Screenshot from 2022-03-13 14-50-49](https://user-images.githubusercontent.com/727070/159783447-505c0c93-5567-47d7-a2f6-df2e83c3f929.png)

The frequency of this waveform is modulated.
It starts inaudibly low. Then when the game starts, it follows an upward curve until a limit.
When the "high speed" button is pressed it momentarily drops in frequency, then follows a quick upward curve, and follows a downward curve when it is released, like so:
![Screenshot from 2022-03-13 21-25-05](https://user-images.githubusercontent.com/727070/159783769-c6b143d7-2896-4b4d-aaae-8686b150a79e.png)

Based on this information we were able to come up wih an implementation strategy:
* Turn the waveform into an array
* Turn the frequency response curve into trhee lookup tables:
  * One for the start of the game
  * One for when the "high speed" button is pressed
  * One for when the "high speed button is not pressed
* Follow the frequnce curve as needed, according to the current state.


### Bonus

The bonus sound seemed simple at first, but turned out to be more complicated than we thought.
When the bonus input goes high shortly, and then low. The sound is quite simple, like so:
![Screenshot from 2022-03-16 10-57-04](https://user-images.githubusercontent.com/727070/159784788-b70a5f67-6db0-4cf8-be79-bdd09e51bb1b.png)
We came up with a algorithm to describe this sound, and implemented it in a SystemVerilog module.
#### The algorithm:

> Bonus is a pulse generator, that goes to 100% amplitude immediately when the bonus pin goes high. \
> The pulse is always running, just multiplied by an amplitude.

> When the bonus pin goes low, the sound decreases in volume following a an exponential curve. \
> When the bonus pin is low, the pulse period is 3/4 of the length, resulting in a [perfect fourth](https://en.wikipedia.org/wiki/Perfect_fourth) \
> The amplitude halves every 28 ms so it's something like: \
> Amplitude = MaxAmplitude-((0.976^time_in_miliseconds)*MaxAmplitude)

> The pulse period when the bonus pin is high has length 0.002746s, and it's high 75% of the time \
> so equivalent to a loop of: \
> {1,1,1,0} \
> The final result looks like it goes through a very slight low pass filter. \
> at 48khz, results in a loop of: \
> {97{2}, 1, 33{0}, 1}

MaxAmplitude should be set to the highest number that fits, to keep precision.
Normally I use fixed point math with 32 of precision, for multiplications like this.
Later we will convert to 16 bits precision, for the output.

We implemented in SystemVerilog this like so:

```
module bonus(
    input clk,
    input clk_48KHz_en,
    input bonus_en,
    output reg[15:0] audio_out = 0
);

    localparam MAX_AMPLITUDE = 1 << 18 << 14;
    reg[1:0] WAVEFORM_SLOW[131:0];
    reg[1:0] WAVEFORM_FAST[98:0];
    assign WAVEFORM_SLOW[97] = 1;
    assign WAVEFORM_SLOW[131] = 1;
    assign WAVEFORM_FAST[73] = 1;
    assign WAVEFORM_FAST[98] = 1;

    genvar i;
    generate
        for (i = 0; i <= 96; i = i + 1) begin
            assign WAVEFORM_SLOW[i] = 2;
        end
        for (i = 98; i <= 130; i = i + 1) begin
            assign WAVEFORM_SLOW[i] = 0;
        end
    endgenerate

    genvar j;
    generate
        for (j = 0; j <= 72; j = j + 1) begin
            assign WAVEFORM_FAST[j] = 2;
        end
        for (j = 74; j <= 97; j = j + 1) begin
            assign WAVEFORM_FAST[j] = 0;
        end
    endgenerate
    

    localparam AMPLITUDE_RATIO_PER_TIMESTEP_18 = 262008; // z^(28ms*48khz) = 0.5, so z = 0.99948, 0.99948 * 2^18 = 262008

    reg[9:0] current_sample = 0;
    reg[68:0] amplitude = 0;

    reg last_bonus_en = 0;

    localparam SLOW_TO_FAST_RATIO_16 = 87381; // 4/3 * 2^16 = 87381.3333333
    reg[15:0] map_slow_to_fast = ((current_sample * SLOW_TO_FAST_RATIO_16) >> 16);

    always_ff @(posedge clk) begin
        if(clk_48KHz_en)begin
            last_bonus_en <= bonus_en;

            if(bonus_en)begin
                amplitude <= MAX_AMPLITUDE;

                if(current_sample == 131)begin
                    current_sample <= 0;
                end else begin
                    current_sample <= current_sample + 1;
                end
                audio_out <= (amplitude * WAVEFORM_SLOW[current_sample]) >> 18;
            end else begin 
                if(last_bonus_en)begin
                    current_sample <= map_slow_to_fast;
                    audio_out <= (amplitude * WAVEFORM_SLOW[current_sample]) >> 18;
                end else begin
                    if(current_sample >= 98)begin
                        current_sample <= 0;
                    end else begin
                        current_sample <= current_sample + 1;
                    end
                    audio_out <= (amplitude * WAVEFORM_FAST[current_sample]) >> 18;
                end
                amplitude <= (AMPLITUDE_RATIO_PER_TIMESTEP_18 * amplitude) >> 18;
            end

        end 
    end

endmodule
```

But it turned out that this was not the whole story.
At the end of the game, the bonus pin goes high for a longer time, which triggers a different effect, where the frequency of the tone gets modulated in a more complex way.
We had to go back to simulation, where it turned out that the NOT gated at the bottom had the wrong voltage threshold assigned to them.

![wrong_invertors](https://user-images.githubusercontent.com/727070/159786529-51d6f7bd-57a0-4f9f-b888-b836ebb3aff6.png)

While this did not change the short bonus sound, which the machine makes when a jewel is picked up, it does change the sound when the bonus pin goes high for a longer period.
It seemed like the Falstad simulator wasn't fast enough to do the simulation, but after tuning the initial voltages of the capacitors, the system got into a simulatable state.

![Screenshot from 2022-03-29 22-00-42](https://user-images.githubusercontent.com/727070/160696976-e89c10a8-2051-4c26-b3e5-3299ddca835b.png)

This was what came out of the simulation, which gave some insight about which frequencies to use.
But listening to the recordings from teh real cabinet there were still some differences:
* the real sound goes up and down faster
* the real sound stays low longer and high shorter
* the real sound has a slide between the fequencies 

The simulation also has a slide going from high to low, but it is more prominent/slower the real recording.

Also with this improved simulation, the blip sound when coins are picked up turned out to be slightly different.

The amplitude goes down, before the frequency goes up.

![Screenshot from 2022-03-29 22-02-47](https://user-images.githubusercontent.com/727070/160697288-17550eac-e8ff-492b-b408-5827683d6457.png)

Aslo the frequency of the high tone is higher than we originally thought, we checked in the recordings from the real cabinet, where it was also higher.

Based on these new findings we improved our implementation of the bonus sound:

```
module bonus(
    input clk,
    input clk_48KHz_en,
    input bonus_en,
    output reg[15:0] audio_out = 0
);

    localparam MAX_AMPLITUDE = 1 << 18 << 14;
    reg[1:0] WAVEFORM_SLOW[131:0];
    reg[1:0] WAVEFORM_FAST[98:0];
    assign WAVEFORM_SLOW[97] = 1;
    assign WAVEFORM_SLOW[131] = 1;
    assign WAVEFORM_FAST[57] = 1;
    assign WAVEFORM_FAST[78] = 1;

    genvar i;
    generate
        for (i = 0; i <= 96; i = i + 1) begin
            assign WAVEFORM_SLOW[i] = 2;
        end
        for (i = 98; i <= 130; i = i + 1) begin
            assign WAVEFORM_SLOW[i] = 0;
        end
    endgenerate

    genvar j;
    generate
        for (j = 0; j <= 56; j = j + 1) begin
            assign WAVEFORM_FAST[j] = 2;
        end
        for (j = 58; j <= 77; j = j + 1) begin
            assign WAVEFORM_FAST[j] = 0;
        end
    endgenerate
    

    localparam AMPLITUDE_RATIO_PER_TIMESTEP_18 = 262008; // z^(28ms*48khz) = 0.5, so z = 0.99948, 0.99948 * 2^18 = 262008

    reg[32:0] current_sample = 0;
    reg[68:0] amplitude = 0;

    reg last_bonus_en = 0;
    reg[15:0] bonus_en_ago = 0;

    localparam SLOW_TO_FAST_RATIO_16 = 39222; // 79/132 * 2 ^ 16 = 39222.3030303
    reg[32:0] map_slow_to_fast = ((current_sample * SLOW_TO_FAST_RATIO_16) >> 16);

    reg[32:0] bonus_en_length = 0;

    always_ff @(posedge clk) begin
        if(clk_48KHz_en)begin
            if(bonus_en || bonus_en_ago < (11 * 132))begin
                bonus_en_length <= bonus_en_length + 1;

                if(current_sample == 131)begin
                    current_sample <= 0;
                end else begin
                    current_sample <= current_sample + 1;
                end

                if(bonus_en_length >= 55 * 132)begin
                    if(current_sample >= 78)begin
                        current_sample <= 0;
                        audio_out <= (amplitude * WAVEFORM_FAST[0]) >> 18;
                    end else begin
                        current_sample <= current_sample + 1;
                        audio_out <= (amplitude * WAVEFORM_FAST[current_sample]) >> 18;
                    end
                    if(bonus_en_length == 75 * 132) begin
                        bonus_en_length <= 0;
                    end
                end else begin
                    audio_out <= (amplitude * WAVEFORM_SLOW[current_sample]) >> 18;
                end

                if(~bonus_en)begin
                    bonus_en_ago <= bonus_en_ago + 1;
                    last_bonus_en <= 1;
                    amplitude <= (AMPLITUDE_RATIO_PER_TIMESTEP_18 * amplitude) >> 18;
                end else begin
                    amplitude <= MAX_AMPLITUDE;
                    bonus_en_ago <= 0;
                end
            end else begin
                if(last_bonus_en)begin
                    bonus_en_length <= 0;
                    last_bonus_en <= 0;
                    current_sample <= map_slow_to_fast;
                    audio_out <= (amplitude * WAVEFORM_FAST[map_slow_to_fast]) >> 18;
                end else begin
                    if(current_sample >= 78)begin
                        current_sample <= 0;
                    end else begin
                        current_sample <= current_sample + 1;
                    end
                    audio_out <= (amplitude * WAVEFORM_FAST[current_sample]) >> 18;
                end
                amplitude <= (AMPLITUDE_RATIO_PER_TIMESTEP_18 * amplitude) >> 18;
            end

        end 
    end

endmodule
```

The only thing that is missing now, is the slide between the frequencies. It is left for later improvement.

### Crash

The crash sound consists of a noise source that switches two oscilators on and off. The oscilators are based on 555 timers, which are out of tune, that go through their own signal path.

An in-depth analysis:

![head_on_crash_in-depth-analysis](https://user-images.githubusercontent.com/727070/160704801-faf1123c-df04-4792-9176-5bb00a8cff4d.png)

We simulated the circuit:

![Screenshot from 2022-03-29 23-09-07](https://user-images.githubusercontent.com/727070/160707551-d4f028c8-d2e4-44f2-b904-6001d6a5877a.png)

The real noise source is a 18 bit lsfr, in the simulation we used a built-in noise source of the simulator, but it worked out nicely. It took some tweaking and improving to get the simulation to work, but it sounded like the real thing in the end.

It's a difficult sound to convert into an algorithm. It would probably involve some kind of sine continuation like found in the [bang sound of red baron](https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/rtl/bang_sound.sv), but it's not exactly clear to us how the opamp circuits here work.

