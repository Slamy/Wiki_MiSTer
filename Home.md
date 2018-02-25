# Welcome to the MiSTer wiki!

_DISCLAIMER: this is an open project without focus on sales. Base hardware (Terasic DE10-Nano) can be bought from major electronic component resellers and will run a few cores out of the box. No soldering is needed_ 

_DISCLAIMER2: Many cores require RAM expansion hardware which can be assembled or bought from a few sources in the forums. The author of this project and contributors are NOT affiliated to these vendors and do not derive any income from it. Please direct any inquiries or concerns about expansion hardware to relevant third parties_

![photo](pictures/MiSTer.jpg)

## What is it?

MiSTer is a port of well known MiST project to a larger FPGA and faster ARM. MiSTer provides modern video output through HDMI (VGA and analog audio are still available on daughter board). It's based on [**Terasic DE10-nano**](http://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=167&No=1046) board.
Here are some improvement over the MiST board:

* Altera Cyclone V SE FPGA with 110,000LE (41,500ALM) and 5,570Kbit of Block RAM.
* ARM Cortex A9 dual-core CPU at 800MHz.
* HDMI video and audio allowing connect to any modern monitor/TV.
* DDR3 1GB available for both ARM and FPGA.
* High speed ARM<->FPGA interconnect due to both are in the same chip.
* Linux on ARM provides support for many I/O devices and file systems.
* Board is mass produced by a big manufactured and freely available for a relatively cheap price 130USD (99USD for students/professors).

Due to a larger FPGA, bigger systems can be created. It's also possible to add more support from ARM side. For example TZX tape format can be parsed on ARM and then send to FPGA. Firmware is not limited by code size or available RAM. It'e even possible to emulate some parts of system on ARM which is not available in FPGA (so-called hybrid emulator). 

MiSTer scales original video resolution to a standard HDMI resolution (usually 1280x720p60), so you don't need to look for some ancient monitor with VGA input supporting non-standard resolution and frame rates. For purists VGA is still available and it outputs original video resolution.

## How does it work?

MiSTer uses [3 daughter boards](https://github.com/MiSTer-devel/Hardware_MiSTer):
* **SDRAM board**. This is a small boards plugged into GPIO0 connector of the DE10-nano board. Although DE10-nano has fast DDR3 memory, it cannot be used to emulate a retro EDO DRAM due to a high latency and shared usage from ARM side. So, SDR SDRAM on daughter board is required for most cores to emulate a retro memory.
* **I/O board**. This board is plugged into GPIO1 connector of the DE10-nano board. It provides a legacy VGA output (6 bits per component), analog audio (3.5mm phone jack), digital optical audio, buttons, LEDs. This board is optional. It's useful if you prefer VGA over HDMI or you want to put the board to some case. Also this board is useful for core development because HDMI scaler code requires around twice more time to compile the core. Thus compiling for VGA-only will speed up the development.
* **RTC board**. This board is plugged into LTC connector. Provides the real time clock. It's optional board. You still can have the real time clock without the board if MiSTer is connected to internet.

Schematics and gerber files are available. Boards are considered as DIY(do it yourself). There are no restrictions who and how these board will be manufactured and sold, so any 3rd party is welcome to manufacture and sell it.

Talking about the Linux, most people will think "Oh, Linux will take a lot of time to load." It's not true in this case. The Linux used on this board is specially tweaked and takes only 2 seconds to boot. Usually monitor/TV requires longer time to lock the video and start to display. So usually board is ready sooner than TV start to display the video.

## More info
Discussion about the project is [here](http://www.atari-forum.com/viewforum.php?f=117)