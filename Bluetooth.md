# MiSTer supports Bluetooth input devices.

Supported devices: Gamepads, Keyboards, Touch pads(as a part of multifunctional keyboard). Support for mouse and standalone touch pads is unclear. Need to be tested.

Bluetooth host must be a standalone USB BT dongle. Multifunctional dongles such as WiFi+BT probably won't work. Confirmed to work dongles based on CSR8510 and BCM20702 chips. Most (if not all) BT dongles you can buy today are based on these chips.

## BT pairing dialog.
Either press and hold OSD button on I/O board for 3 seconds, or F11 key (only when OSD is active).

## Pairing for gamepads and keyboards
* Put your gamepad/keyboard into pairing mode.
* Invoke BT pairing dialog.
* MiSTer will try to find and pair the device (Keyboards require to enter pin 0000 and press enter).

## Pairing for Dualshock 3 and Sixaxis gamepads
* Connect the gamepad through USB to MiSTer.
* Press PS button and wait for lights stop to blinking and only one remain active.
* Disconnect the gamepad - lights will start to blink and then only one will remain active if succeeded.

Note: Dualshock 4 gamepad is a standard BT gamepad. So follow the first paring method.

## Notes:
- Only single BT dongle is supported.
- Depends on environment condition (how many WiFi spots and active BT devices are around) you may connect more or less BT devices at the same time. In my place i could successfully connect 3 BT devices at the same time. The 4th one couldn't be connected till i turn off one of connected. Other BT dongle allowed only 2 gamepads at the same time.
- After MiSTer reboot many BT devices won't re-connect automatically. Some devices will shutdown them selves immediately, other devices need to be turned off manually then on.
