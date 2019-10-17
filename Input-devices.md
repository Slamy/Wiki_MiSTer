# Selecting good controllers for your MiSTer
MiSTer supports many different USB input devices such as keyboards, joysticks, gamepads, and mice. A keyboard can emulate other input devices (so basically it is enough to control all cores).

A wireless combo keyboard (keyboard with touchpad) and wireless game pad is a nice set to control MiSTer and play games.

For some notes on selecting a good input device, please read the advice in [Selecting Input Devices](Selecting-Input-Devices).

### Joystick assignment
Up to 6 controllers are supported (depending on core):
* After a core starts, press a button on a connected controller to make it the P1 gamepad/joystick
* Press a button on a second controller to make it the P2 joystick (if supported by core)
* Keep going for P3, P4, etc.

### USB Joystick mapping
USB joysticks, gamepads, and keyboards need to be defined in the central menu before use in any core.
Please refer to [Main Joystick Mapping](Core-Joystick-Mapping)

### Auto fire
Any defined button (except d-pad) supports **auto fire** feature. To activate auto fire, press and keep desired button and then quickly press the button defined as "BUTTON OSD"(for joystick) or "KBD TOGGLE"(for keyboard). To deactivate auto fire, repeat the the same procedure.

Auto fire provides 50ms-1000ms rates. To choose the speed, press and keep one of direction on d-pad and then quickly press the button defined as "BUTTON OSD"(for joystick) or "KBD TOGGLE"(for keyboard).

### Mouse emulation
Joystick can emulate mouse if required button **"Mouse Emu"** has been defined in default joystick definition (Menu core).
Hold **"Mouse Emu"** button and **"Alt/M"**, **Mouse Left/Right/Middle Btn** will emulate the mouse functions. Also defined analog stick for mouse will be switched to pointer functions. Press **"BUTTON OSD"** while holding **"Mouse Emu"** to toggle mouse emulation permanently. In permanent mouse emulation "Mouse Emu" button becomes a **sniper button** (smaller pointer movements). Only buttons defined for mouse emulation will be switched. Other joystick buttons will continue to act as joystick buttons. Thus, if your game pad has many buttons, you can have both mouse and joystick in one game pad at the same time (useful for some games, like Walker on Amiga).

### Notes:
* Joystick actions can be viewed in [serial console](Console-connection) while running Menu core.

# Mouse
Most mouses/trackballs/touchpads should work. Up to 3 buttons are supported (depend on core).

# Keyboard
Keyboards can support key re-mapping, mouse emulation, and joystick emulation.
See [Keyboard](Keyboard) for details