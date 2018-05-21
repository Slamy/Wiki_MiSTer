## There are only 3 things you need to start with the platform:

## (1) Board
The heart and engine of the whole platform is the **Terasic DE10-nano** development board.

You can buy it:
* Directly from [Terasic](http://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&No=1046&PartNo=8)
* [Mouser](http://www.mouser.com/ProductDetail/Terasic-Technologies/P0496/)
* [Digikey](https://www.digikey.com/product-detail/en/terasic-inc/P0496/P0496-ND/6817231)

An 8GB Micro-SD card is included with the kit, it can be reformatted to use with your MiSTer.
Any MicroSD card 2GB and larger should work fine as well. Speed class doesn't affect it.

## (2) USB connection
It is recommended that you use a powered OTG USB hub with your DE10-nano board. The socket isn't very robust so it is better to avoid connecting and disconnecting too often. It is also not able to handle high current consumption, so any powered USB devices will need an external powered hub. It handles a keyboard and mouse fine, though.

### USB option 1:
**Micro USB OTG cable + USB 2.0 hub.**
USB 2.0 hub with external power might be a good idea both to eliminate OTG socket reliability issues and provide power to external devices. Some cheap ones on e-bay/aliexpress may be declared as full speed USB 2.0 but in fact work in USB low speed mode. Acceptable for keyboard, but better avoid them.

### USB option 2:
**OTG USB Hub.** These hubs are designed to connect directly to micro-USB OTG port and require less inter-connections cables. Such HUBs are also available on e-bay/aliexpress.

### USB option 3:
**[USB hub daughter board.](https://github.com/MiSTer-devel/Main_MiSTer/wiki/USB-Hub-daughter-board)** You can assemble this board that provide 7 usb ports available to the MiSTer system.


## (3) Optional part. Expansion boards
Several cores require an external **SDR SDRAM board** expansion to work, since they require more accurate memory timings than the BRAM and DDR3 RAM integrated in the DE10-nano. As such it is strongly recommended that you build or buy an SDRAM board to use the MiSTer fully. 

There is also an **I/O board** to provide more capabilities like VGA output for old monitors, analog audio, optional audio out, and Buttons/LEDs for external connections to integrate into existing old computer cases. This board is fully optional (no core strictly requires it) but it may be convenient to plug audio output outside of HDMI (for example)