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

clk_sys is the system clock. Make sure to use the same clock when reading from these signals.
HPS_BUS should be passed through from the top level emu.

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
	input             clk_sys,
	inout      [45:0] HPS_BUS,

```

## Joystick input

MiSTer supports up to 6 players on separate joysticks. joystick_0..5 are digital joysticks. They contain the directions in the first 4 bits, and then they have buttons that can be mapped using the CONF_STR J. 

* joystick_x[0] - right
* joystick_x[1] - left
* joystick_x[2] - down
* joystick_x[3] - up

Analog joysticks are supported by connecting joystick_analog_x. The values are analog -127..+127, Y: [15:8], X: [7:0] . Depending on how you want to use the values, you may need to renormalize them. -128 is omitted so it is easier to invert the direction.

Paddles - paddle_x - are input devices that have a range from 0 to 255. They do not spin fully.

Spinners - spinner_x - are a paddle looking device, but there is no stop in the hardware, they spin freely. Therefore, these use an extra bit 8 that toggles with each update. the value is in 0:7, -128..+127 - they are relative, and usually the value will be between -8 and 8.

```Verilog
	// buttons up to 32
	output reg [31:0] joystick_0,
	output reg [31:0] joystick_1,
	output reg [31:0] joystick_2,
	output reg [31:0] joystick_3,
	output reg [31:0] joystick_4,
	output reg [31:0] joystick_5,
	
	// analog -127..+127, Y: [15:8], X: [7:0]
	output reg [15:0] joystick_analog_0,
	output reg [15:0] joystick_analog_1,
	output reg [15:0] joystick_analog_2,
	output reg [15:0] joystick_analog_3,
	output reg [15:0] joystick_analog_4,
	output reg [15:0] joystick_analog_5,

	// paddle 0..255
	output reg  [7:0] paddle_0,
	output reg  [7:0] paddle_1,
	output reg  [7:0] paddle_2,
	output reg  [7:0] paddle_3,
	output reg  [7:0] paddle_4,
	output reg  [7:0] paddle_5,

	// spinner [7:0] -128..+127, [8] - toggle with every update
	output reg  [8:0] spinner_0,
	output reg  [8:0] spinner_1,
	output reg  [8:0] spinner_2,
	output reg  [8:0] spinner_3,
	output reg  [8:0] spinner_4,
	output reg  [8:0] spinner_5,
```

## 