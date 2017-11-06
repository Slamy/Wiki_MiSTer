# General info
MiSTer supports many different USB input devices such as keyboards, joysticks, gamepads, and mice. A keyboard can emulate other input devices (so basically it is enough to control all cores).

A wireless combo keyboard and wireless game pad is a nice way to control MiSTer and play games.

# Game controllers - Joysticks and Gamepads

### Joystick assignment
P1 and P2 controllers are currently supported:
* After a core starts, press a button on a connected controller to make it the P1 gamepad/joystick
* Press a button on a second controller to make it the P2 joystick (if supported by core)

### Joystick mapping
MiSTer provides a flexible mechanism for button configuration. Buttons defined in the Menu core are the default button mapping for all cores, but you can also define buttons separately for each core. This mapping is recommended for maximum compatibility.

Mapping settings are specific to each device (identified by USD VID and PID), and apply regardless of whether it is the P1 or P2 controller (this means you can map them all then switch order by resetting the core).

The number of button supported per core varies (1 to 7 currently). While defining buttons, you can press "space" to skip (keep undefined) the button, "ESC" to cancel, and "Enter" to stop mapping  (i.e. make the rest of buttons undefined).

### Auto fire
Any defined button (except d-pad) supports **auto fire** feature. To activate auto fire, press and keep desired button and then quickly press the button defined as "BUTTON OSD"(for joystick) or "KBD TOGGLE"(for keyboard). To deactivate auto fire, repeat the the same procedure.

Auto fire has 4 speeds. To choose the speed, press and keep one of direction on d-pad and then quickly press the button defined as "BUTTON OSD"(for joystick) or "KBD TOGGLE"(for keyboard).

### Mouse emulation
Joystick can emulate mouse if required button **"Mouse Emu"** has been defined in default joystick definition (Menu core).
Hold **"Mouse Emu"** button and **"Alt/M"** direction buttons with **R/L/M.Button** will emulate the mouse functions. Also analog joystick **axis 0/1** will be switched to pointer functions regardless of definitions. Press **"BUTTON OSD"** while holding **"Mouse Emu"** to toggle mouse emulation permanently. In permanent mouse emulation "Mouse Emu" button becomes a **sniper button** (smaller pointer movements). Only buttons defined for mouse emulation will be switched. Other joystick buttons will continue to act as joystick buttons. Thus, if your game pad has many buttons, you can have both mouse and joystick in one game pad at the same time (useful for some games, like Walker on Amiga).


### Notes:
* in OSD navigation: first defined button is "select", second(if has) is "cancel", third(if has) is "back".
* In Menu core, joystick definition has (Alt/M) directions definition which used as alternative direction buttons in all cores in addition to directions defined in particular core. Alt/M directions will be switched to mouse functions in mouse emulation mode. You can define Alt/M directions and L/R/M.Button to the same buttons/sticks as main directions/buttons - in this case mouse mode will take these buttons for mouse emulation.
* While defining joystick buttons, you can press "SPACE" key on keyboard to skip the button (make it undefined) if you have not enough buttons or current function/button is not required.
* Technical info: supported directional mapping of following known analog joy/pad axises: 0/1(val: 0..255), 2/5(val: 0..255), 16/17(val: -1,0,1).
* Joystick actions can be viewed in [serial console](Console-connection) while running Menu core

# Mouse
Most mouses/trackballs/touchpads should work. Up to 3 buttons are supported (depend on core).

# Keyboard
MiSTer supports keys re-mapping which is useful for reduced or localized keyboards. Key remapping is system wide, so every core will have same key map. Keep in mind it's not macro definition, so single key is remapped to another single key. Some multimedia keys generate several key codes - these keys cannot be remapped.
Each keyboard model has its own key map stored in **/config/kbd_[VID]_[PID].map** file. To reset all keys to default state, simply delete appropriate map file. Key remapping is available through Menu core only.

### Joystick emulation
Keyboard can be switched to joystick emulation. You need to define keys used for joystick emulation the same way you did for joysticks. Auto fire is also supported the same way as for joysticks. Button defined for "KBD TOGGLE" provides a quick switch between keyboard and joystick for defined keys.

### Mouse emulation
Keyboard can be switched to mouse emulation. You need to define mouse emulation buttons in Menu core the same way as for joystick.

### Emulation switch
To switch between emulation modes press **NumLock** or **ScrLock** till desired mode is selected. 

Switching sequence is **Mouse >> Joy1 >> Joy2 >> None**

LEDs on keyboard display the emulation modes:
* Mouse emulation: NumLock LED + ScrLock LED
* Joystick 1 emulation: NumLock LED.
* Joystick 2 emulation: ScrLock LED.

### Common functional keys/combos used in cores
* **F12** - open/close OSD menu/submenu
* **Alt-F12** - quick core selection (like in Menu core).
* **LCtrl+LAlt+RAlt** - presses the "USER" button which usually is reset in emulated system.
* **LShift+LCtrl+LAlt+RAlt** - MiSTer reset (load Menu core).


### Notes:
* Some systems provide writing support which requires additional attention to how you reset/shutdown the MiSTer. MiSTer tries not to keep any pending writes and writes physically to the disk as soon as possible. Still, safer way to reset the MiSTer from core which probably was writing to disk recently is using combo **LShift+LCtrl+LAlt+RAlt** - this will flush all caches to disk before restart. Cores without write can be restarted by hard reset button or powered down without special attention.
* LCtrl+LAlt+RAlt sequence can be replaced by some other well known combos through INI file.
