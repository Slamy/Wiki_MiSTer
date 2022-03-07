Many old computers have analog parts, for example audio boards that have partly analog synthesis and old desktop computers with tape input.

Currently there is no convenient way to directly simulate electronic circuits, for example based in their spice netlists, in real time on the MiSTer.
So to implement these type of circuits in fpga, you will have to come up with some kind of simulation of the behavior of the electronic circuit.

The [Arcade-Battlezone](https://github.com/jopdorp/Arcade-BattleZone_MiSTer) core is an example of a core with analog sound synthesis.

A way to approach the problem:

1. Identify the digital and analog parts of the schematic.
1. Implement all the digital parts
1. Identify analog circuit with isolated behavior, i.e. 1 input, 1 output.
1. Identify easily recognisable parts, such as low pass filters, high pass filters and mixers. 