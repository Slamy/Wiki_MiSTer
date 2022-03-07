Many old computers have analog parts, for example audio boards that have partly analog synthesis and old desktop computers with tape input.

Currently there is no convenient way to directly simulate electronic circuits, for example based in their spice netlists, in real time on the MiSTer.
So to implement these type of circuits in fpga, you will have to come up with some kind of simulation of the behavior of the electronic circuit.

The [Arcade-Battlezone](https://github.com/jopdorp/Arcade-BattleZone_MiSTer) core is an example of a core with analog sound synthesis.

A way to approach the problem:

1. Find youtube video's of people playing the actual game, to get some idea of the sounds it has.
1. Play the game in an emulator, paying extra attention to sounds that do not sound the same in the emulator as in the video of the actual machine
1. Identify the digital and analog parts of the schematic.
1. Implement all the digital parts
1. Identify analog circuit with isolated behavior, i.e. 1 input, 1 output.
1. Identify easily recognisable and implementable parts, such as:
   1. low pass filters
   1. high pass filters
   1. (inverting) amplifiers
   1. mixers

1. All the parts that are going to need more attention, make note of what these parts are an try to guess what they are for.
1. Implement the mixers
1. Implement the filters
1. Implement the difficult parts of the circuit:
   1. Implement the circuit in a simlator.
   1. Figure out what input goes into the circuit when the game gets played.
   1. Is the input always the same? (not noise as input) Does the circuit always response in the same way? (not generating noise)
      1. Sample the output of the simulation
      1. Convert the sample into an array literal and trigger it as needed, usually the sample will just be triggered by a pulse in this case.
   1. If the analog circuit has noise as input or has variable inputs such as a number controlled frequency or speed you will need to make a mathematical model of the sound.
