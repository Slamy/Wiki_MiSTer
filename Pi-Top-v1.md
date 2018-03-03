This is an attempt to put MiSTer into Pi-Top (v1, original) case and make a MiSTer notebook.

### This is not a budget case.
Case is pretty expensive but the only solution on the market. High price of the case doesn't mean good quality, alas. Plastic used on the case is so-so. Connections between plastic details aren't good either. Be careful as some parts are easy to brake (although pi-top site is full of pictures with children). Overall it looks like cheap case, but as has been said, there is no other option on the market to make your own notebook. 

You can think about adaptation of some (old) notebook case. But it will be more hard and possibly even more expensive. Notebook displays usually have either LVDS or eDP interface while Pi-Top has HDMI. So you will need to find/make a conversion board for notebook display which is not always possible. Keyboard and touchpad in traditional notebook have "naked" interfaces providing low-level connection while Pi-Top provides USB connection for both keyboard and touchpad. So you will need to make another conversion board for keyboard and touchpad on traditional notebook. Battery management on traditional notebook is on main board, so another board is required while Pi-Top provides integrated HUB board to manage the battery and display power control. So, adaptation of traditional notebook will require pretty large board to convert internal interfaces to those compatible with MiSTer(DE10-nano). Different notebooks have different internals, so it's impossible to make a one board for all notebook cases. And usually even in old thick notebooks there is no much space to fit DE10-nano - especially in height dimension.

So, after judge all these difficulties, the only viable option is Pi-Top case.

### There are 2 versions of Pi-Top cases.
Please note: this project is targeted to v1 (called as original on Pi-Top site) case only. This version has more space inside and has no specific to RPi holes and places. So, we have pretty relaxed placement of DE10-nano inside. Semi-transparent cover gives good view to all DE10-nano LEDs and doesn't require to drill the holes. v1 uses railed holes to fix the boards, while v2 case uses magnet rails not suitable for this project.

Probably it's possible to use v2 case as well, but it will require completely different add-on boards. 

v2 is available only in childish acid green color which is a main distraction point.

### You need to be very careful while messing with internals.
* There is high voltage on HUB board and its connector. It's highly advised to de-solder and remove pin 1 on PiTopHUB (pictures are coming) connector. It delivers 16.5V and very dangerous for DE10-nano. There is no usage of 16.5V so it's better to remove this pin (picture is coming). Connector on PiTopHUB isn't shrouded and it's very easy to shift it while connecting and fry everything!
* Many parts on PiTopHUB are powered even when main power of Pi-Top is turned off. It's result of bad Pi-Top design. So, you need to be careful. Don't drop any metallic parts on the board. Avoid to touch the board.

### Buggy MCU firmware.
While developing the boards for Pi-Top i found it's easy to make MCU on PiTopHUB to stick in non-responsible state. And since MCU is always powered (even in power off state) power cycle isn't enough. There are 2 ways to reset the MCU.
1. Remove PiTopHUB and effectively remove the power from MCU.
2. Carefully short the two lower pins on tiny 6-pin connector (picture is coming) - this is reset of MCU.

### New releases required.
New releases of Linux. MiSTer binary and Cores are required. Releases after March 02 2018 will be compatible with Pi-Top. 
Display of Pi-Top supports only one resolution - 1920x1080. So every core will require to support this resolution.

### Butter-smooth video
Although Pi-Top display supports only single resolution, it accepts any (reasonable) pixel clock and refresh rate. So, with this display and automatic VSync adjust option video may have original retro system refresh rate. All scrollers will be very smooth.

## Required Boards
Gerber and PDF files for all boards can be found [here](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/master/releases)

### [Main Board](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/master/Addons/IOBoard_PiTopAIO)
This board has all important parts such as memory, both SD cards and Audio. 
### Memory
Both SDRAM (32MB) and SRAM (2MB) are on this board, although SRAM is not supported by any core. There are no plans to use SRAM in foreseen future, so it's advised not to solder SRAM and save the cost.
### SD Cards
Board has the same secondary SD card as on original MiSTer board. Another SD card is original DE10-nano card through micro-SD extender (pictures are coming) providing convenient access to card as original is in hard to reach place.
### Audio
Audio amplifiers may be soldered directly on board by components, or using [Adafruit audio breakout boards](https://www.adafruit.com/product/3006) by soldering connectors points. MAX98357A has very tiny pads - if you are not sure in your soldering capability, use the breakout boards. The price is about the same as set of components.
Although board has places for audio amplifier, it's advised not to solder it. Audio amplifiers gives up to 3.2W per channel and may draw up to 1.2A from 5V source. Due to audio nature, the draw will not be constant and will hammer the DE10-nano power circuit. So, it's advised to solder audio amplifiers on separate Audio board. 
By default 5V power of audio is connected to 5V of DE10-nano. There is an option to use external 5V supply for audio by cutting tiny cut point near P6 connector and connect external 5V (take from Audio/Connection board) source to unload internal DE10-nano power circuit.

### Notes
Due to height limit in Pi-Top case, this board is mounted at some angle. P1 uses standard profile connector while P2 uses high profile connector (same as on standard MiSTer I/O Board). Thus one side of Arduino connector will slightly protrude from this board's cutout while other side will be covered by the board. You need to cut pins on both connectors at the board level before soldering to make sure it won't prevent closing of sliding cover. (pictures are coming)
P4(primary card extender) and I2S_FPGA (if you use audio board) are better to be soldered as SMD using exposed pads on the bottom of the board for the same reason.(pictures are coming)

### [Audio Board](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/master/Addons/PiTopAudio) or [Connection Board](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/master/Addons/PiTopConn)
Use only one of these boards. Connection board is stripped down version of Audio board used in case when audio amplifiers are on Main Board. If unsure, use audio board. You can leave audio part unsoldered and use it as simple connection board.

Audio amplifiers may be soldered directly on board by components, or using [Adafruit audio breakout boards](https://www.adafruit.com/product/3006) by soldering connectors points. MAX98357A has very tiny pads - if you are not sure in your soldering capability, use the breakout boards. The price is about the same as set of components.

Besides audio amplifiers, the boards are providing I2C and SPI connections to DE10-nano (through RTC board). I2C is used for battery monitoring. SPI is used for display brightness control. It's also providing power for fan. Fan power circuit has flexible way to adjust the power using diodes and resistors (see schematics).

### [RTC Board](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/master/Addons/RTC)
RTC v1.3(or higher) is required to provide I2C and SPI connections. You don't need to populate the board if RTC is not required. You may connect I2C/SPI directly to DE10-nano without RTC board using 14-pin cable connector - just follow the RTC schematics.

### [USB HUB Board](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/master/Addons/PiTopUSBHub)
This board provides convenient USB device connections - both internal and external. The board is in developing stage, gerber fill be release after testing.
This is optional board. You may use any tiny USB HUB to connect devices as you like.
