This page contains commonly asked questions and their answers.

**Table of Contents**
- [When will MiSTer support cartridges?](#when-will-mister-support-cartridges)
- [Does MiSTer have lag?](#does-mister-have-lag)
- [Any USB controller recommendations?](#any-usb-controller-recommendations)
- [Can I use native controllers?](#can-I-use-native-controllers)
- [Does my MiSTer need cooling?](#does-my-mister-need-cooling)
- [Does MiSTer need an IO board?](#does-mister-need-an-io-board)
- [Do I need an IO board to get analog video output to my CRT?](#do-i-need-an-io-board-to-get-analog-video-output-to-my-crt)
- [Do I need a Hub Add-On Board?](#do-i-need-a-hub-add-on-board)
- [I heard the DE10-Nano board uses subsidized components. Is MiSTer doomed if that stops?](#i-heard-the-de10-nano-board-uses-subsidized-components-is-mister-doomed-if-that-stops)


##  When will MiSTer support cartridges?

MiSTer will never use physical cartridges. 

Not only is it outside the scope of the project which aims to replace the need for having real hardware, it is physically very impractical/impossible given the number of GPIO pins available from the FPGA.

## Does MiSTer have lag?

_Short answer:_ No, not with the right peripherals. 

_Long answer:_ You may see some latency depending on your display, controller and settings. But they can all be tweaked to a large extent if that is important to you.  [See here](lag-explained)

## Any USB controller recommendations?

Please refer to [this page](Selecting-Input-Devices)

## Can I use native controllers?

_Short answer:_ Yes.

_Long answer:_ Native controllers can be used with a USB adapter.  There are a few specialized controllers that may not work as a regular gamepad (eg. Zapper), and for those it is possible to use a serial interface board (e.g. IO Board + SNAC). Native protocols via SNAC are currently supported for NES, SNES, and Genesis cores. Through this, a Zapper can be used with a CRT.


## Does MiSTer need an IO board?

_Short answer:_ No.

_Long answer:_ The IO board is optional, but offers some features that might be important to some users.  Being an Input/Output (IO) device, it’s primary function is to provide a native (like original hardware) video and audio signal to analog displays (CRTs) with zero lag (see FAQ 2 above) and audio devices via 3.5mm audio cable or optical (TOSLINK) output.  Please note, HDMI video and audio will continue to function when using analog output.  This dual output is especially useful for those who wish to capture/stream gameplay footage.  The input side of the device refers to the serial port, which has the same physical appearance as a USB 3.0 port.  It is not however, a true USB port, and does not support regular USB devices at all.  See FAQ 4 above for more information on how you would use this part of the IO board.  There are other small features of the IO board that serve minor purposes; please see [this page](IO-Board) for more information about them.

## Do I need a Hub Add-On Board?

_Short answer:_ No.

_Long answer:_ The USB Hub Addon Board can be considered a luxury item.  An inexpensive OTG USB HUB from online markets will work fine for many people.  The advantage of the addon board is that it physically integrates very cleanly and safely with the DE10 and it has seven powered USB ports which is plenty for almost any user.  Users who want to use many or several power hungry USB devices will want to at least be sure to get a USB Hub that is externally powered so as not to overtax the DE10’s power circuitry.  Take care to pay attention to the DE10’s rather delicate OTG USB port.  Another advantage of the addon board is that it very securely attaches to this port.  Corded OTG Hub users will want to be careful that this port is not stressed by a sudden jerk or a slow steady pull.

## Does my MiSTer need cooling?

_Short answer:_ Yes, at least a heatsink (passive cooling). 

_Long answer:_ While it's fine for general operations, the DE-10 board’s FPGA chip ideally requires a passive heatsink to avoid heat interfering with some of the more complex cores.  22mm x 22mm is the ideal heatsink size for this.  Active cooling (a fan) is recommended for long term use.  Some cores may present corruption/artifacts if the chip is not cooled with a fan.  A 40mm diameter fan, powered from either the IO board or directly from one of the DE-10’s GPIO pins, is the recommended type for this task.  Typically this fan is mounted on the optional IO board, however it can also be mounted on a 3D-printed plate or hand-cut piece of plastic or cardboard if you do not need or have an IO board.

## Do I need an IO board to get analog video output to my CRT?

_Short answer:_ No.  You can use an HDMI to VGA adapter to do it.

_Long answer:_ Use of an inexpensive HDMI to VGA adapter is supported in most cores. These dongles can easily be found in online markets by searching.


## I heard the DE10-Nano board uses subsidized components. Is MiSTer doomed if that stops?

No. The DE10 Nano is broadly sold to universities and is available in larger supply than custom hardware made only for retro enthusiasts. In general, these development boards are manufactured and sold for a long time (the last generation DE1 board is still sold), so there is no reason to be concerned. Worst case, the work done in cores can be ported to other boards in the future. For now, the DE10-Nano remains the best and most cost-effective option, and MiSTer is a perfect fit for it as the boards are intended to introduce FPGA programming to a wider audience.



