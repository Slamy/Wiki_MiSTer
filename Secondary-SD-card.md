## Introduction
Some cores require low-level SD card access. The primary SD card cannot provide low-level access due to incompatible layout. It is also locked by Linux system from direct access. Thus, I/O board v5.x provides the secondary SD card which is directly connected to FPGA. Linux system doesn't see this card. The layout of the secondary SD card is fully depend on core requirements. Usually it's simple FAT16 format, but some cores may require custom formatting.

## Schematics
Secondary SD card is simple direct connection between SD connector and DE10-nano GPIOs. It's possible to solder by yourself if whole I/O Board is not required (or older I/O Board is used). Check the [schematic](https://github.com/MiSTer-devel/Hardware_MiSTer/raw/master/releases/iobrd_5.2.pdf) if you want to connect it by yourself.

## Support
Following cores require the secondary SD card:
* MSX
* Atari 800
* Atari 5200
* Sharp X68000
* Sinclair QL (not confirmed yet)

More cores will support the secondary SD card.