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
1. Identify common, easily recognisable and implementable parts, such as:
   1. low pass filters https://www.electronics-tutorials.ws/filter/filter_2.html
![low pass](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/1st_Order_Lowpass_Filter_RC.svg/250px-1st_Order_Lowpass_Filter_RC.svg.png)   
   1. high pass filters https://www.electronics-tutorials.ws/filter/filter_3.html
![high pass](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fe/High_pass_filter.svg/250px-High_pass_filter.svg.png)
   1. inverting amplifiers
![inverting amplifier](https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/Op-Amp_Inverting_Amplifier.svg/250px-Op-Amp_Inverting_Amplifier.svg.png)
   1. non inverting amplifiers
![non inverting amplifier](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Op-Amp_Non-Inverting_Amplifier.svg/250px-Op-Amp_Non-Inverting_Amplifier.svg.png)
   1. differential amplifiers
![differential amplifier](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Op-Amp_Differential_Amplifier.svg/250px-Op-Amp_Differential_Amplifier.svg.png)
   1. other common opamp circuits: https://en.wikipedia.org/wiki/Operational_amplifier_applications
   1. additive mixers
![additive mixer](https://upload.wikimedia.org/wikipedia/en/thumb/5/5a/Passive_Mixer.jpg/250px-Passive_Mixer.jpg)


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


Handy links:
* For finding the right values of a filter: https://www.micromodeler.com/dsp/
* Common operational amplifier uses, such as differentiators and integrators: https://en.wikipedia.org/wiki/Operational_amplifier_applications