This is an attempt to put MiSTer into Pi-Top (v1, original) case and make a MiSTer notebook.

### This is not a budget case.
Case is pretty expensive but the only solution on the market. High price of the case doesn't mean good quality, alas. Plastic used on the case is so-so. Connections between plastic details aren't good either. Be careful as some parts are easy to brake (although pi-top site is full of pictures with children). Overall it looks like cheap case, but as has been said, there is no other option on the market to make your own notebook. 

You can think about adaptation of some (old) notebook case. But it will be more hard and possibly even more expensive. Notebook displays usually have either LVDS or eDP interface while Pi-Top has HDMI. So you will need to find/make a conversion board for notebook display which is not always possible. Keyboard and touchpad in traditional notebook have "naked" interfaces providing low-level connection while Pi-Top provides USB connection for both keyboard and thouchpad. So you will need to make another conversion board for keyboard and touchpad on traditional notebook. Battery management on traditional notebook is on main board, so another board is required while Pi-Top provides integrated HUB board to manage the battery and display power control. So, adaptation of traditional notebook will require pretty large board to convert internal interfaces to those compatible with MiSTer(DE10-nano). Different notebooks have different internals, so it's impossible to make a one board for all notebook cases. And usually even in old thick notebooks there is no much space to fit DE10-nano - especially in height dimension.

So, after judge all these difficulties, the only viable option is Pi-Top case.

### There are 2 versions of Pi-Top cases.
Please note: this project is targeted to v1 (called as original on Pi-Top site) case only. This version has more space inside and has no specific to RPi holes and places. So, we have pretty relaxed placement of DE10-nano inside. Semi-transparent cover gives good view to all DE10-nano LEDs and doesn't require to drill the holes. v1 uses railed holes to fix the boards, while v2 case uses magnet rails not suitable for this project.

Probably it's possible to use v2 case as well, but it will require completely different add-on boards. 

v2 is available only in childish acid green color which is a main distraction point.

### You need to be very careful while messing with internals.
* There is high voltage on HUB board and its connector. It's highly advised to de-solder and remove pin 1 on PiTopHUB (pictures are coming). It delivers 16.5V and very dangerous for DE10-nano. There is no usage of 16.5V so it's better to remove this pin (picture is coming). Connector on PiTopHUB isn't shrouded and it's very easy to shift it while connecting and fry everything!
* Many parts on PiTopHUB are powered even when main power of Pi-Top is turned off. It's result of bad Pi-Top design. So, you need to be careful. Don't drop any metallic parts on the board. Avoid to touch the board.

### Buggy MCU firmware.
While developing the boards for Pi-Top i found it's easy to make MCU on PiTopHIB to stick in non-responsible state. And since MCU is always powered (even in power off state) power cycle isn't enough. There are 2 ways to reset the MCU.
1. Remove PiTopHUB and effectively remove the power from MCU.
2. Carefully short the two lower pins on tiny 6-pin connector (picture is coming) - this is reset of MCU.

## Required Boards
### Main Board
(TBA)
### Audio Board or Connection Board
(TBA)
### RTC Board
(TBA)
### USB HUB Board
(TBA)
