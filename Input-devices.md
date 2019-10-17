# Selecting good controllers for your MiSTer
MiSTer supports many different USB input devices such as keyboards, joysticks, gamepads, and mice. A keyboard can emulate other input devices (so basically it is enough to control all cores).

A wireless combo keyboard (keyboard with touchpad) and wireless game pad is a nice set to control MiSTer and play games.

**WARNING: High performance and expensive keyboards and mice aren't good for MiSTer. They won't give any benefits, so it's just waste of money. Also these devices have too many functions and many virtual devices cluttering input subsystem which may introduce input lag or be complete unresponsive. They may prevent other devices such as gamepads to work. So try to avoid these gaming Chrismass-Tree like keyboards and mice. Buy a simple one.**

# Game controllers - Joysticks and Gamepads

**PS3,PS4,X360,XOne** gamepads are known to have problem with MiSTer. These gamepads have accelerometers and constantly sends the events with high rate. Analog sticks also send events even when not touched. Overall MiSTer receives huge flood of event from these controllers. These events may prevent correct button definition. Games may behave incorrectly when using these controllers. 

The ideal solution today for these gamepads is to use 3rd-party receivers such as 8bitdo retro receivers, specifically the **8Bitdo Wireless Bluetooth Adapter**. It not only gives you wireless access, but also filters out all these unneeded events, while supporting Xbox One S/X, PS3, PS4, Wii, Switch, and 8Bitdo's own gamepads. One receiver will pair with one controller at one time. If multiple controllers are required for multiplayer games, then multiple receivers will need to be purchased.

The Grey/Orange (brick decorated) USB Adapters are functionally the same, after using the latest firmware. Gamepads may switch to different input modes using hotkeys for different functionality. Note that documentation on 8Bitdo's site doesn't specify this, but the update logs for the firmware updates does.

- X-Input mode: Hold SELECT+UP for 3 seconds.
- PSC (Playstation Classic) mode: Hold SELECT+DOWN for 3 seconds. This is useful for gamepads which are limited in buttons (12 total; DPAD counts as 4) and need to access the MiSTer OSD menu. Note that the OSD menu should not be assigned when configuring buttons in the main MiSTer menu core, as the L+R+START combination will bring up the OSD while in the cores. The combination is hard-coded in MiSTer specifically for 8Bitdo adapters. You may also lose auto-fire/mouse functionality in this mode.

Alternative 8Bitdo adapters, such as the 8Bitdo Console Retro Receiver (SNES, NES, Genesis) are always in X-Input mode when connected via microUSB.

**Bluetooth Adapters and Dongles:**  
Any off-the-shelf bluetooth dongles will work with most wireless controllers like Dualshock4, Xbox, 8Bitdo.  
See [Bluetooth](Bluetooth) for details

### Joystick assignment
Up to 6 controllers are supported (depending on core):
* After a core starts, press a button on a connected controller to make it the P1 gamepad/joystick
* Press a button on a second controller to make it the P2 joystick (if supported by core) and so on.

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