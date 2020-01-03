## You only need 4 things to start with MiSTer:

* [DE10-Nano board](DE10-Nano-board) (required)
* [USB connection](How-to-start-with-MiSTer#2-usb-connection) (required)
* [Expansion boards](How-to-start-with-MiSTer#3-optional-part-expansion-boards) (optional)
* [Cooling](How-to-start-with-MiSTer#4-cooling-fpga) (recommended)

Obviously, it is assumed you would already have at least a basic HDMI monitor or TV for video and audio output, and a USB keyboard for basic input. 

## 1. DE10-Nano board
The heart and engine of the whole platform is the **Terasic DE10-Nano** development board, made in Taiwan.

You can buy it:
* Directly from [Terasic Inc.](http://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&No=1046&PartNo=8)

Or from major electronics suppliers such as:
* [Mouser](http://www.mouser.com/ProductDetail/Terasic-Technologies/P0496/)
* [Digikey](https://www.digikey.com/product-detail/en/terasic-inc/P0496/P0496-ND/6817231)

A power supply unit (PSU) and 8GB MicroSD card is included with the kit. The SD card can be reformatted to use with your MiSTer.
Any MicroSD card 2GB and larger should work fine as well. Speed class doesn't affect it.

## 2. USB connection
It is recommended that you use a powered OTG USB hub with your DE10-Nano board. The socket isn't very robust so it is best to avoid connecting and disconnecting too often. It is also not able to handle high current consumption, so any powered USB devices will need an external powered hub. If you're not connecting too many USB peripherals, it does handle a keyboard, mouse, and gamepad just fine.

### USB option 1:
**Micro USB OTG cable + USB 2.0 hub.** 

USB 2.0 hub with external power might be a good idea both to eliminate OTG socket reliability issues and provide power to external devices. Some cheap ones on e-bay/aliexpress may be declared as full speed USB 2.0 but in fact work in USB low speed mode. Acceptable for keyboard, but better avoid them.

### USB option 2:
**OTG USB Hub.** 

These hubs are designed to connect directly to micro-USB OTG port and require less inter-connection cables. Such HUBs are also available on e-bay/aliexpress.

### USB option 3:
**[USB hub daughter board.](https://github.com/MiSTer-devel/Main_MiSTer/wiki/USB-Hub-daughter-board)** 

You can assemble our purchase this board that provides 7 USB ports available to the MiSTer system.


## 3. Optional Expansion boards 

Several cores require an external **[SDRAM board](https://github.com/MiSTer-devel/Main_MiSTer/wiki/SDRAM-Board)** expansion to work, since they require more accurate memory timings than the BRAM and DDR3 RAM integrated in the DE10-Nano. As such, it is highly recommended that you build or purchase a SDRAM board to realise the full potential of MiSTer. 

There is also an optional **[I/O board](https://github.com/MiSTer-devel/Main_MiSTer/wiki/IO-Board)** to provide more capabilities like VGA output for old monitors, analog audio, optional audio out, and Buttons/LEDs for external connections to integrate into enclosures. 

This board is fully optional (no core strictly requires it) but it may be convenient to plug audio output outside of HDMI (for example). 


## 4. Cooling FPGA 

The hybrid ARM+FPGA chip has been found to get hot when "working", even idling in the core menu, therefore some passive cooling is recommended. The main heat producer in the chip is the integrated dual-core ARM processor producing a constant heat regardless the FPGA core in use. 

The Cyclone V FPGA chip on the DE10-Nano board is industrial grade and supports up to 100°C, but for guaranteed long term usage without degrading its characteristics,  it's highly advisable to add at least a heatsink. 

This chip is approximately 21.5mm x 21.5mm. Ideal dimensions of a heatsink is 22mm x 22mm, and it will cover all the FPGA. Commonly found heatsinks with dimensions ranging from 20mm x 20mm to 25mm x 25mm can be used,  but for larger heatsinks pay attention to nearby components, they must not touch the heatsink. 

The height of the heatsink should be no more than 10mm if an I/O board is used because it could touch parts in the I/O board and create short circuits.

### Active cooling 

Some large cores such as ao486 and Minimig are sensitive to FPGA chip temperature and become unstable if it becomes too hot. So active cooling, in addition to passive cooling, is required for stability. 

If you're building or purchasing an [I/O board](https://github.com/MiSTer-devel/Main_MiSTer/wiki/IO-Board), they are designed for a 40mm x 40mm fan. Assembled I/O boards should already have a fan installed. 

If you do not use any I/O boards then you are free to choose any fan, but bear in mind that only 5V is available from the Terasic DE10-Nano board, so a 5V fan is required. You may also consider a larger 12V fan, they should work but spin slower and still provide good airflow. 


A large selection of fans can be found on most electronic components sites, such as [DIGIKEY](https://www.digikey.co.uk/products/en/fans-thermal-management/dc-fans/217?FV=38007c%2Cffe000d9%2Cb89e93&quantity=0&ColumnSort=0&page=1&pageSize=25&pkeyword=40mm+fan), Mouser and others.

