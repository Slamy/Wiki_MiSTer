## You only need 4 things to start with MiSTer:

* DE10-Nano board (required)
* USB connection (required)
* Expansion boards (optional)
* Cooling (recommended)

## (1) Board (DE10-Nano)
The heart and engine of the whole platform is the **Terasic DE10-Nano** development board.

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
Several cores require an external **[SDR SDRAM board](https://github.com/MiSTer-devel/Main_MiSTer/wiki/SDRAM-Board)** expansion to work, since they require more accurate memory timings than the BRAM and DDR3 RAM integrated in the DE10-nano. As such it is strongly recommended that you build or buy an SDRAM board to use the MiSTer fully. 

There is also an **[I/O board](https://github.com/MiSTer-devel/Main_MiSTer/wiki/IO-Board)** to provide more capabilities like VGA output for old monitors, analog audio, optional audio out, and Buttons/LEDs for external connections to integrate into existing old computer cases. This board is fully optional (no core strictly requires it) but it may be convenient to plug audio output outside of HDMI (for example)


## (4) Cooling FPGA
The hybrid ARM+FPGA chip gets hot when "working", even in menu core so some passive cooling is required. The main heater in the chip is dual-core ARM producing a constant heat regardless the FPGA core. The version of chip on the board is industrial grade and basically supports up to 100C degrees, but for guaranteed long usage without degrading the characteristics it's highly advised to use the cooler. FPGA used in Terasic DE10-Nano board is approximately 21.5mm x 21.5mm. Ideal dimension of heatsink is 22mm x 22mm millimeters and it will cover all the FPGA. 
A 25mm x 25mm can be used but pay ATTENTION to nearby components, they must not touch the heatsink. The height of the heatsink should be no more than 10 mm if a I/O board is used because it could touch parts in the I/O board making short circuits.

### Active cooling
Some large cores like ao486 and Minimig are sensitive to FPGA chip temperature and become unstable if it's hot. So active cooling, in addition to passive cooling, is required for better stability.
Latests [I/O boards](https://github.com/MiSTer-devel/Main_MiSTer/wiki/IO-Board) do have a place for a 40mm x 40mm fan.
If you do not use any I/O boards then you can use bigger fans, but bear in mind that only 5V is available from Terasic DE 10 Nano board, so a 5V fan is required.
Assembled [I/O boards](https://github.com/MiSTer-devel/Main_MiSTer/wiki/IO-Board) already have a fan installed so no problems.
If you do not use I/O boards or you want to add a fan you can find it on electronic components sites like [DIGIKEY](https://www.digikey.co.uk/products/en/fans-thermal-management/dc-fans/217?FV=38007c%2Cffe000d9%2Cb89e93&quantity=0&ColumnSort=0&page=1&pageSize=25&pkeyword=40mm+fan) or others.

