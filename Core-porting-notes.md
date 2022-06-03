# Introduction

MiSTer uses quite complex hardware, but thanks to open source, developers with different levels of hardware/software knowledge can develop for this platform. Many cores for MiSTer use common code simplifying access to hardware and firmware called **Framework**.
We will use the [Template](https://github.com/MiSTer-devel/Template_MiSTer) core in this guide.

## Framework
Most of the sources of the Framework are located in the [`sys`](https://github.com/MiSTer-devel/Template_MiSTer/tree/master/sys) folder. 
Usually, for a new project, you need the following files/folders
* `sys` folder
* `mycore.qpf` (project file. Keep it read-only.)
* `mycore.qsf`
* `mycore.srf` (some warnings ignored)
* `mycore_Q13.qsf`
* `mycore_Q13.srf` (some warnings ignored)

You'll need to make some changes:
* Rename `mycore.*` files according to your project.
* Inside files, replace `mycore` with the name of your project.
* `*.qsf` files contain list of project files. Remove files not related to your project.

The initial set of files for your project is now ready. Now you can open the project in Quartus 17.0 or higher. 
Assuming you are porting an existing core to MiSTer, the top module entity should be renamed to `emu`. See `mycore.sv` and its input/output signals:
```Verilog
module emu
(
	//Master input clock
	input         CLK_50M,

	//Async reset from top-level module.
	//Can be used as initial reset.
	input         RESET,

	//Must be passed to hps_io module
	inout  [45:0] HPS_BUS,

	//Base video clock. Usually equals to CLK_SYS.
	output        CLK_VIDEO,

	//Multiple resolutions are supported using different CE_PIXEL rates.
	//Must be based on CLK_VIDEO
	output        CE_PIXEL,

	//Video aspect ratio for HDMI. Most retro systems have ratio 4:3.
	//if VIDEO_ARX[12] or VIDEO_ARY[12] is set then [11:0] contains scaled size instead of aspect ratio.
	output [12:0] VIDEO_ARX,
	output [12:0] VIDEO_ARY,

	output  [7:0] VGA_R,
	output  [7:0] VGA_G,
	output  [7:0] VGA_B,
	output        VGA_HS,
	output        VGA_VS,
	output        VGA_DE,    // = ~(VBlank | HBlank)

	output        LED_USER,  // 1 - ON, 0 - OFF.

	// b[1]: 0 - LED status is system status ORed with b[0]
	//       1 - LED status is controled solely by b[0]
	// hint: supply 2'b00 to let the system control the LED.
	output  [1:0] LED_POWER,
	output  [1:0] LED_DISK,

	output [15:0] AUDIO_L,
	output [15:0] AUDIO_R,
	output        AUDIO_S, // 1 - signed audio samples, 0 - unsigned


	//High latency DDR3 RAM interface
	//Use for non-critical time purposes
	output        DDRAM_CLK,
	input         DDRAM_BUSY,
	output  [7:0] DDRAM_BURSTCNT,
	output [28:0] DDRAM_ADDR,
	input  [63:0] DDRAM_DOUT,
	input         DDRAM_DOUT_READY,
	output        DDRAM_RD,
	output [63:0] DDRAM_DIN,
	output  [7:0] DDRAM_BE,
	output        DDRAM_WE,

	//SDRAM interface with lower latency
	output        SDRAM_CLK,
	output        SDRAM_CKE,
	output [12:0] SDRAM_A,
	output  [1:0] SDRAM_BA,
	inout  [15:0] SDRAM_DQ,
	output        SDRAM_DQML,
	output        SDRAM_DQMH,
	output        SDRAM_nCS,
	output        SDRAM_nCAS,
	output        SDRAM_nRAS,
	output        SDRAM_nWE

        // there are more needed signals - see the Template_MiSTer
);
```
These signals are main connections to MiSTer. You'll need to modify your core according to these signals.


### API
Most top-level signals should be self-descriptive and more or less familiar to core developers, so I won't go too deep into it. I will describe some important parts where you need to pay attention to make your core work.

```verilog
input   RESET
```
This signal is asserted while ARM part is under initial preparation. It can be used as an initial reset. It won't be asserted anymore during the whole work of core except when the user chooses another core from OSD. Then ARM will assert `RESET` in the existing core to let it stop any possible activity before switching to another core (cores loaded through USB Blaster won't get "bye-bye" reset).
If core uses DDR3 memory (scaler isn't counted) then initial and bye-bye reset are crucial for correct operation. You will get a hard hang if DDR3 is accessed during RESET.

```verilog
inout  [45:0] HPS_BUS
```
Pass it as-is to `hps_io` module.

```verilog
output        CLK_VIDEO,
output        CE_PIXEL,
output  [12:0] VIDEO_ARX,
output  [12:0] VIDEO_ARY,
output        VGA_DE,
```
Besides other well-known `VGA_*` signals, these signals are important in MiSTer in order to get a proper display. `CLK_VIDEO` and `CE_PIXEL` are used to sample the pixels. If pixel rate equals to `CLK_VIDEO`, then set `CE_PIXEL` to `1`. Many cores have a common system clock where pixel frequency is the product of the division of system clock by some number. In this case, set `CLK_VIDEO` to the system clock and assert `CE_PIXEL` at clock cycles where a new pixel is produced. Look in `mycore.sv` to see how it's done.
Without `CLK_VIDEO`, you can still have VGA output, but OSD won't work.

`VIDEO_ARX` and `VIDEO_ARY` define aspect ratio on HDMI output. It doesn't affect VGA output. Usually `VIDEO_ARX=4`/`VIDEO_ARY=3` or `VIDEO_ARX=16`/`VIDEO_ARY=9`. Other values are possible, but extreme values may cause video problems.

`VGA_DE` is another crucial part for MiSTer. Basically, it's opposite of blank signals `~(VBlank | HBlank)` but with some notes. HDMI video scaler detects the horizontal resolution by first active video line. So, you need to be sure the first line is not cut due to misaligned VBlank and HBlank signals. Otherwise, you'll get a distorted HDMI video.

`VGA_HS` and `VGA_VS` should have positive pulse polarity.

```verilog
output        AUDIO_S
```
Make sure you set correct mode signed/unsigned, otherwise audio will be distorted.

`DDRAM_` are signals for DDR3 memory. If the core can use this memory instead of SDRAM, then an SDRAM board is not required.

`SDRAM_` are signals for SDRAM memory. The core will require an SDRAM board if these signals are used.


### HPS_IO
The supplementary module `hps_io.v` is also required (see `mycore.sv`). It provides input/output control from the ARM side. Most signals are the same or similar to those in MiST (`user_io`/`data_io` or `mist_io` modules). So, if the core is ported from MiST, the signals will be mostly identical.

MiSTer has some changes/improvements over the original MiST I/O modules:
* Support for up to four mounted images (MiST only supports one). Set module parameter `VDNUM` to `2..4` if more than one mounted image is required. If `VDNUM` is set to `1`, then related signals are same as in MiST.
* Due to the SD card using multiple partitions, cores are unable to access the entire SD card. Only access to ROM files is possible. Cores requiring direct access to SD card should be redesigned for access to ROMs only.
* Main MiSTer partition is formatted as exFAT, which supports files bigger than 4GB.
* OSD supports up to 15 lines (7 lines in MiST) which is handy for many cores.
* Communications between ARM and FPGA are performed via the parallel bus, which speeds up communication. It supports 16bit I/O.
* Other under-the-hood improvements to firmware, such as keyboard/mouse/joystick setup.
