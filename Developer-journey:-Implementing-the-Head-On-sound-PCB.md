# Developer journey: Implementing the Head On sound PCB
This page contains a description of how we implemented the sound PCB of the game Head On from SEGA/Gremlin.

## First steps
We analyzed the schematics of the Head On sound PCB board. Identifying circuits for individual sounds, and repeated parts of the circuit.
![head-on audio board analysis](https://user-images.githubusercontent.com/727070/159781502-7407a16c-356e-4d6b-8e8b-e0f9c0b8f8aa.png)
We talked about what we thought is what, and decided to start with the car sound.

## Finding real footage
Searching the web for video's with the sounds, we found a couple, but the quality was bad:
https://discord.com/channels/@me/950484205664612402/951108401801338890
https://discord.com/channels/@me/950484205664612402/951139287745851425

JimmyStones contacted the maker of the sound board, to see if he had some tips. He seemed willing to help, but not familiar enough with the fpga domain to join the project.
The JimmyStones found someone who own a cabinet and was able to obtain some good sound recordings.

This gave us a way to validate our results.

## Simulating and analyzing
### Car
We started by implementing the car sound in the falstad simulator.
It took some tweaking, mostly getting things like the diode type and transistor beta values right.
We managed to get a result that sounded pretty much like the real deal.
This is the final circuit:
[car_circuit.txt](https://github.com/MiSTer-devel/Main_MiSTer/files/8336074/car_circuit.txt)
it can be loaded into the [falstad simulator](https://www.falstad.com/circuit/)
Frow there it is possible to record a wav file, which we used to analyze the sound.

It turns out that the car sound consists of a repeating waveform that looks like this:
![Screenshot from 2022-03-13 14-50-49](https://user-images.githubusercontent.com/727070/159783447-505c0c93-5567-47d7-a2f6-df2e83c3f929.png)

The frequency of this waveform is modulated.
It starts inaudibly low. Then when the game starts, it follows an upward curve until a limit.
When the "high speed" button is pressed it momentarily drops in frequency and follows a quick upward curve, and follows a downward curve when it is released, like so:
![Screenshot from 2022-03-13 21-25-05](https://user-images.githubusercontent.com/727070/159783769-c6b143d7-2896-4b4d-aaae-8686b150a79e.png)

Based on this information we were able to come up wih an implementation strategy:
* Turn the waveform into an array
* Turn the frequency response curve into trhee lookup tables:
  * One for the start of the game
  * One for when the "high speed" button is pressed
  * One for when the "high speed button is not pressed
* Follow the frequnce curve as needed, according to the current state.


### Bonus


