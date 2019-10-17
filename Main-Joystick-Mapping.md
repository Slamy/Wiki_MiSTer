**Before you can use any joystick with MiSTer cores, it is necessary to map it to system-wide buttons on the menu core.**

Following types of input are defined in Menu core:
* **DPAD test**. Test the type of DPAD. Some gamepads generate analog stick events, so it's important step. Simply press the RIGHT button on DPAD. In case if it generates analog stick event, it will ask to press the DOWN at the second stage or will skip it if no analog event has been detected. If you define the keyboard keys for joystick emulation, then simply press the RIGHT arrow key and it will skip Stick 1/2 steps and jump to DPAD keys definition.
* **Stick 1 and 2 analog axes**. If your joystick has no analog sticks then skip it by SPACE key. Otherwise you need to define them to get proper analog to digital mapping. (**Note:** Some gamepads like 8bitdo M30 emulate analog stick events on DPAD, so you have to press RIGHT and DOWN for Stick 1! Skip for Stick 2) These definitions have no relation to any specific map. It only tells to MiSTer these axes have min-0-max values with 0 as a default position and will be mapped to 2 digital buttons at the both ends. Other analog axes not defined here will be treated as 0-max with only 1 digital button.
* **Right,Left,Down,Up,Btn1..Btn4**. Basic buttons.
* **Right,Left,Down,Up (Alt/Mouse)** - alternative direction control. If your gamepad has analog stick, then you can assign it here. In cores this alternative control will work in parallel to the one defined in the core. So you will be able to control directions with DPAD(or whatever you've defined in core) and analog stick. Some games are good to be controlled by stick, other games are good with DPAD. These controls are used for mouse emulation as well, so if you don't have the stick (or don't want to use it), then define DPAD buttons here again.
* **Mouse Left/Right/Mid Btn** - buttons for mouse emulation. If your gamepad has many buttons then you can define separate buttons for mouse only, so when in mouse emulation mode both joystick and mouse buttons will be available at the same time. On reduced gamepads you may define the same buttons used for Btn1..Btn4.
* Mouse Emu/Sniper - button to switch to mouse emulation. While holding it down gamepad will emulate the mouse. In permanent mouse mode (press OSD button while in temporary mouse mode) this button is used for smaller pointer steps (sniper mode).
* **BUTTON OSD** - important button used to access OSD menu and some additional functions.
* **Stick X/Y** - analog axes. Some cores support or even require analog joystick. For gamepads usually it's left stick.
* **Mouse emu X/Y** - analog axes for mouse emulation. You may use the same stick as for Stick X/Y if only one analog stick is available. For dual sticks gamepad you may use the other stick, so in mouse emulation mode both mouse directions and joystick directions will be available at the same time. With enough buttons and sticks defined as 2 separate sets for joystick and mouse, you can play games requiring the joystick and mouse at the same time like Walker on Amiga.

You also need to define the buttons in each core where you want to use this joystick. Each core may have its own buttons layout.

**Note:** Keyboard can be used as joystick. So you have to define the keyboard as joystick in both Menu core and the core you want to use!

Mapping settings are specific to each device (identified by VID and PID). If you have several identical gamepads/joysticks then they will share the same button layout.

The number of button supported per core varies (up to 32). While defining buttons, you can press "SPACE" to skip (keep undefined) the button, "ESC" to cancel, and "Enter" to stop mapping  (i.e. make the rest of buttons undefined).