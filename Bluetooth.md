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

## Notes / Troubleshooting
- Only single BT dongle is supported.
- Depends on environment condition (how many WiFi spots and active BT devices are around) you may connect more or less BT devices at the same time. In my place i could successfully connect 3 BT devices at the same time. The 4th one couldn't be connected till i turn off one of connected. Other BT dongle allowed only 2 gamepads at the same time.
- After MiSTer reboot many BT devices won't re-connect automatically. Some devices will shutdown them selves immediately, other devices need to be turned off manually then on.
- Bluetooth support was added to MiSTer_20190406. Make sure to update the Linux image, menu core and mister main. As of 2019-4-17 the [updater script](https://github.com/MiSTer-devel/Updater_script_MiSTer) doesn't update the Linux image by default, use the [SD Installer](https://github.com/MiSTer-devel/SD-Installer-Win64_MiSTer) to update the base Linux image.
- Spotty connections and difficulty pairing have been reported with non-powered USB hubs. A powered USB hub is always recommend.
- BCM20702 BT dongles may stuck in RF unresponsive state after reboot. From driver point of view device looks like working, but none of BT devices able to connect. Currently the only fix is to re-plug the dongle. CSR based dongles have no such issue.