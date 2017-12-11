MiSTer provides an on-screen display (OSD) that can be toggled on and off by pressing F12 on your keyboard (or OSD button). For each core that is loaded, this menu can be configured to add specific options for that core.

The top-level module for the cores is `emu`. This does **NOT** mean `emu` is the top-level module for the project, but rather it is the top-level module for our purposes. The `emu` module is typically found in the SystemVerilog file (*\*.sv extension*) with the same name as the project. As an example, the Arcade-Galaga project has it's top-level module at *Arcade-Galaga.sv*.

The configuration string is stored in the variable *CONF_STR* of the *emu* module. This variable is passed to the *hps_io* module that handles sending it to the processor to be read when necessary.

Each line of the configuration string is delimited with a semicolon. The first line is the core name followed by semicolon and parameters for F option. F option can be skipped by second semicolon if no F is required or you want to use other than 1st line for F option.

Here are the follow valid options for the menu ([] - means optional parameter):
* T{Index},{Name} - Trigger button. This is a simple button that will pulse HIGH of specified {index} bit in status register. A perfect example of this is for a reset button. {Name} is the text that describes the button function.
* O{Index1}[{Index2}],{Name},{Options...} - Option button that allows you to select between various choices. {Index1} and {Index2} are values from 0-9 and A-V (like Hex but it extends from A-V instead of A-F). This represents all 31 bits. First and second index are the range of bits that will be set in the status register. {Name} is what is shown to describe the option. {Options...} is a list of comma separated options.
* J[1],{Button1}[,{Button2},...] - J1 means lock keyboard to joystick emulation mode. Useful for keyboard-less systems such as consoles. {Button1},{Button2},... is list of joystick buttons used in the core. Up to 12 buttons can be listed.
* V,{Version String} - Version string. {Version String} is the version string. Takes the core name and appends version string for name to display.
* \- - Skips line.
* F,{Ext}[,{Text}] - Load file button. {Ext} is a string of 3 character extensions. For example, BINGEN would be BIN and GEN extensions. Optional {Text} string is the text that is displayed before the extensions like "Load RAM". If {Text} is not specified, then default is Load \*.
* S{Slot},{Ext}[,{Text}] - Mount SD card button. {Slot} is a value from 0-3. Up to four images can be mounted at the same time. {Ext} - same as in F option. Optional {Text} string is the text that is displayed before the extensions like "Load RAM". If {Text} is not specified, then default is Mount \*.
