There are only 3 things you need to start with the platform:

**1. Board**
The heart and the engine of the whole platform is Terasic DE10-nano development board.

You can purchase:
* Directly from Terasic - http://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&No=1046&PartNo=8
* Mouser - http://www.mouser.com/ProductDetail/Terasic-Technologies/P0496/
* Digikey - https://www.digikey.com/product-detail/en/terasic-inc/P0496/P0496-ND/6817231

8Gb Micro-SD card included into the kit. You can re-use it for MiSTer.
Any Micro-SD card 2Gb and larger should work fine. Speed class or any other parameters doesn't affect

**2. Micro USB OTG cable**

Required to connect input devices. You need one.
Please note, Micro-USB OTG socket on DE10-nano board is not robust, so better to make cable connections/disconnections less often. One more feature for OTG port on a board - it is not tolerant to high current consumption. So it barely handles USB hub with keyboard and mouse connected.

That's why USB 2.0 hub with external power might be a good idea both to eliminate OTG socket reliability issues and provide power to external devices

**3. USB 2.0 powered hub**

Just buy one. Some cheap ones on ebay/ali may be declared as full speed USB 2.0 but in fact work in USB low speed mode. Acceptable for keyboard, but better avoid them.


## Optional part

**Expansion boards**

Yes, they are optional. Provide SDR SDRAM for the emulation cores that highly depends on memory timings but most of them work fine with BRAM and DDR3 that DE10-nano equipped.

I/O board is to have more capabilities like VGA output for old monitors