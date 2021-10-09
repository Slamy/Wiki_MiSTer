# Introduction

HPS stands for Hard Processor System, or the ARM part of the MiSTer FPGA. The hps_io.sv file contains the hps_io module that talks to the MiSTer binary on the arm side. It provides convenient signals to use in each core that abstract the different types of I/O that the core might need to support.

## Instantiating hps_io

The module has a few parameters that are used to set it up.

* CONF_STR - This is how the HPS reads the OSD configuration string
* PS2DIV - This divides the clk_sys to create a slower clock for the legacy ps2 signals: ps2_kbd_clk_out  etc
* WIDE - This makes the ioctl data and sd_buff signals 8 bit  (WIDE=0) or 16 bit (WIDE=1) if it is wide, ioctl_addr is incremented by 2
* VDNUM - Virtual Device Number - This can be 1 to 4, and will create extra virtual block devices
* BLKSZ - Block Size - set the block size of the block device - 0 = 128, 1 = 256, 2 = 512(default), .. 7 = 16384
* PS2WE - PS2 Write Enable - ??
```Verilog
//
// Use buffer to access SD card. It's time-critical part.
//
// WIDE=1 for 16 bit file I/O
// VDNUM 1..4
// BLKSZ 0..7: 0 = 128, 1 = 256, 2 = 512(default), .. 7 = 16384
//
module hps_io #(parameter CONF_STR, CONF_STR_BRAM=1, PS2DIV=0, WIDE=0, VDNUM=1, BLKSZ=2, PS2WE=0)
(

```