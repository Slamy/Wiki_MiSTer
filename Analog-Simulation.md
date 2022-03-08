## What is the problem?
Many old computers have analog parts, for example audio boards that have partly analog synthesis and old desktop computers with tape input.

Currently there is no convenient way to directly simulate electronic circuits, for example based in their spice netlists, in real time on the MiSTer.
So to implement these type of circuits in fpga, you will have to come up with some kind of simulation of the behavior of the electronic circuit.

The [Arcade-Battlezone](https://github.com/jopdorp/Arcade-BattleZone_MiSTer) core is an example of a core with analog sound synthesis.

## A way to approach the problem:

1. Find youtube video's of people playing the actual game, to get some idea of the sounds it has.
1. Play the game in an emulator, paying extra attention to sounds that do not sound the same in the emulator as in the video of the actual machine
1. Identify the digital and analog parts of the schematic.

   One thing to keep in mind is that the digital parts run at the system clock speed, while the analog parts will be outputting at audio sample rate, i.e. 48khz
1. Implement all the digital parts
1. Identify analog circuits with isolated behavior, i.e. 1 input, 1 output. These can be individually implemented and tested.
1. Identify common, easily recognisable and implementable parts, such as: 
   *  low pass filters https://www.electronics-tutorials.ws/filter/filter_2.html

      ![low pass](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/1st_Order_Lowpass_Filter_RC.svg/250px-1st_Order_Lowpass_Filter_RC.svg.png) 

      This can be implemented using an iir low pass filter, you can find the parameters here:
      https://docs.google.com/spreadsheets/d/1Z2DNhAQyqkDpNVJuzYPk3ZeW4rChxN7fTKsLGvb2r7g/edit#gid=0
      and different implementations here:
      * https://github.com/MiSTer-devel/Arcade-Blockade_MiSTer/blob/main/rtl/audio/blockade_lpf.v
      * https://github.com/MiSTer-devel/Arcade-Blockade_MiSTer/blob/main/rtl/audio/iir_1st_order.v
      * https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/rtl/iir.sv
   * high pass filters https://www.electronics-tutorials.ws/filter/filter_3.html

     ![high pass](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fe/High_pass_filter.svg/250px-High_pass_filter.svg.png)
   * inverting amplifiers

     ![inverting amplifier](https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/Op-Amp_Inverting_Amplifier.svg/250px-Op-Amp_Inverting_Amplifier.svg.png)

     This is essentially a sign inversion of the sample, followed by a multiplication.
   * non inverting amplifiers

     ![non inverting amplifier](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Op-Amp_Non-Inverting_Amplifier.svg/250px-Op-Amp_Non-Inverting_Amplifier.svg.png)
   * differential amplifiers

     ![differential amplifier](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Op-Amp_Differential_Amplifier.svg/250px-Op-Amp_Differential_Amplifier.svg.png)
   * other common opamp circuits: https://en.wikipedia.org/wiki/Operational_amplifier_applications
   * additive mixers

     ![additive mixer](https://upload.wikimedia.org/wikipedia/en/thumb/5/5a/Passive_Mixer.jpg/250px-Passive_Mixer.jpg)


1. All the parts that are going to need more attention, make note of what these parts are an try to guess what they are for. [Differentiators](https://en.wikipedia.org/wiki/Operational_amplifier_applications#Inverting_differentiator) and [integrators](https://en.wikipedia.org/wiki/Operational_amplifier_applications#Inverting_integrator) combined with 555 timers and noise inputs can be tricky.
1. Implement the mixers
1. Implement the filters
1. Implement the difficult parts of the circuit:
   1. Implement the circuit in a simlator.
   1. Figure out what input goes into the circuit when the game gets played.
   1. Run the simulation with the correct input and save the output as a wav file
   1. Analyse the output by looking at it in a wave editor like audacity and listening to it.
   1. Is the input always the same? (not noise as input) Does the circuit always response in the same way? (not generating noise)
      1. Sample the output of the simulation
      1. Convert the sample into an array literal and trigger it as needed, usually the sample will just be triggered by a pulse in this case.
   1. If the analog circuit has noise as input or has variable inputs such as a number controlled frequency or speed you will need to:
      1. make a mathematical model of the analog circuit.
      1. implement the model in an easy to use programming language such as python
      1. compare the output of the mathematical model with the output of the circuit simulation using the same inputs. They have to be close, but not identical, but they should be identical to the hearing.
      1. rework your mathematical model to not have to use any dividers in real time, this is done in two steps 
         1. by algebra
         1. by precalculating any left-over divisions into division lookup-tables
      1. you can also create other kind of lookup tables, for example a sine wave.
      1. implement the mathematical model in HDL
    1. verify the outputs of the HDL with a tesbench
    1. hook up the chip to the rest of our core!


## Handy links:
### Informational resources
* For finding the right values of a filter: https://www.micromodeler.com/dsp/
* Common operational amplifier uses, such as differentiators and integrators: https://en.wikipedia.org/wiki/Operational_amplifier_applications
* https://www.allaboutcircuits.com/textbook/reference/chpt-7/fundamentals-spice-programming/

### Code examples
* example of a noise-based sound python implementation in a notebook:
https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/spice/Red%20baron%20crash%20circuit%20sim.ipynb
* example of a piece of python code that generates a lookup table:
https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/rtl/generate_control_coltages_to_frequency.py
* example of a common digital noise generator:
https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/rtl/noise_source_shell_explo.sv
* example of a sine-based sound that takes noise as input:
https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/rtl/bang_sound.sv
* example of a script that can take the output of a spice simulation and generate a wav file from it:
https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/spice/spicetowav.py
* example of a spice netlist for a noise based sound:
https://github.com/jopdorp/Arcade-BattleZone_MiSTer/blob/sound/spice/bang.cir

### Tooling
* https://www.falstad.com/circuit/
* http://ngspice.sourceforge.net/
* https://www.audacityteam.org/