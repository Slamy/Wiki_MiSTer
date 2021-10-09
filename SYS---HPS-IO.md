# Introduction

HPS stands for Hard Processor System, or the ARM part of the MiSTer FPGA. The hps_io.sv file contains the hps_io module that talks to the MiSTer binary on the arm side. It provides convenient signals to use in each core that abstract the different types of I/O that the core might need to support.

## Instantiating hps_io

The module has a few parameters that are used to set it up.

* CONF_STR - This is how the HPS reads the OSD configuration string
* PS2DIV - This divides the clk_sys to create a slower clock for the legacy ps2 signals: ps2_kbd_clk_out  etc
* WIDE - This makes the ioctl data and sd_buff signals 8 bit  (WIDE=0) or 16 bit (WIDE=1) if it is wide, ioctl_addr is incremented by 2
* VDNUM - Virtual Device Number - This can be 1 to 4, and will create extra virtual block devices
* BLKSZ - Block Size - set the block size of the block device - 0 = 128, 1 = 256, 2 = 512(default), .. 7 = 16384
* PS2WE - PS2 Write Enable - option to use 2 way PS/2 communications. See ao486 core.

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

## Buttons

Buttons from the top level emu are what the hardware sees. Buttons from the hps_io can include emulated button presses from the OSD, HPS, etc.

* buttons[1] is the user button
* buttons[0] is the OSD button

```Verilog
	// I/O board button press simulation (active high)
	// b[1]: user button
	// b[0]: osd button
	output      [1:0] buttons,
```
## Forced Scandoubler

Forced Scandoubler is set to 1 when the user wants the scandoubler turned on.
```Verilog
	output            forced_scandoubler,
```
## Direct Video

Direct Video is set to 1 when the MiSTer is using the hdmi as a VGA port with a proper converter.

```Verilog
	output            direct_video,
```

## Status

The status bits are used by the OSD to provide the core with status that the user picks in the OSD. For example, the status string:
```
	"O1,Colors,NTSC,PAL;",
```
would set status[1] to 0 for NTSC and 1 for PAL.  See the documentation for the CONF_STR to understand all of the OSD options.

* status_menumask - this is used to tell the OSD to turn on and off options using the H or h option. Set bit 0 to effect H0.
* status_in, status_set - when status_set is 1, the hps_io will grab the status_in and use it to change the status bits

```Verilog
	output reg [63:0] status,
	input      [63:0] status_in,
	input             status_set,
	input      [15:0] status_menumask,
```
## Info

* info - ?
* info_req - ?

```Verilog
	input             info_req,
	input       [7:0] info,
```
## Force a new Video mode

* new_vmode - if the core needs to force the system to change video modes, it can set this flag
```Verilog

	//toggle to force notify of video mode change
	input             new_vmode,
```

## Virtual Hard Drives and Block Devices

Hard drive images are loaded with the S option in the OSD. There can be up to 4 images mounted at once if VDUM is set to 4. 1-4 are valid values. 

When an image is mounted a bit is set in img_mounted, and then img_readonly and img_size are valid for that img_mounted. Save these values into a register if you will need them later.

These are block devices, so the way to read or write to them is to first specify the blk, and then specify a rd or wr and it will start to stream addresses through the sd_buff_addr. 

* sd_lba - logical block address - this is the block we want to start accessing
* sd_blk_cnt - number of blocks
* sd_rd - read number of blocks starting at address
* sd_wr - write number of blocks starting at address
* sd_ack - acknowledge ?? (what?)

* sd_buff_addr - byte address
* sd_buff_dout - data from disk
* sd_buff_din[VDNUM] - data to disk
* sd_buff_wr - 

```Verilog
	// SD config
	output reg [VD:0] img_mounted,  // signaling that new image has been mounted
	output reg        img_readonly, // mounted as read only. valid only for active bit in img_mounted
	output reg [63:0] img_size,     // size of image in bytes. valid only for active bit in img_mounted


	// SD block level access
	input      [31:0] sd_lba[VDNUM],
	input       [5:0] sd_blk_cnt[VDNUM], // number of blocks-1, total size ((sd_blk_cnt+1)*(1<<(BLKSZ+7))) must be <= 16384!
	input      [VD:0] sd_rd,
	input      [VD:0] sd_wr,
	output reg [VD:0] sd_ack,

	// SD byte level access. Signals for 2-PORT altsyncram.
	output reg [AW:0] sd_buff_addr,
	output reg [DW:0] sd_buff_dout,
	input      [DW:0] sd_buff_din[VDNUM],
	output reg        sd_buff_wr,
```

## ROM and File loading, NVRAM saving

Boot ROMS are automatically loaded using ioctl lines. You can also have ROMS loaded via the F in the OSD, or via an MRA.  

* ioctl_download - 1 when data is being downloaded. 
* ioctl_index - [15:7] which file type [6:0] file number
* ioctl_wr - high when each byte is valid. 
* ioctl_addr - address of byte from / to file - counts by two if set to wide
* ioctl_dout - data going to core from HPS (ROM)
* ioctl_din - data going to HPS from core - ie: to save NVRAM
* ioctl_upload - indicate there is an active upload
* ioctl_upload_req ?
* ioctl_rd - data is valid to read
* ioctl_file_ext - this is the file extension as a string 
* ioctl_wait - set this flag to 1 if core isn't ready to process another byte from the HPS (flow control)

```Verilog
	// ARM -> FPGA download
	output reg        ioctl_download = 0, // signal indicating an active download
	output reg [15:0] ioctl_index,        // menu index used to upload the file
	output reg        ioctl_wr,
	output reg [26:0] ioctl_addr,         // in WIDE mode address will be incremented by 2
	output reg [DW:0] ioctl_dout,
	output reg        ioctl_upload = 0,   // signal indicating an active upload
	input             ioctl_upload_req,
	input      [DW:0] ioctl_din,
	output reg        ioctl_rd,
	output reg [31:0] ioctl_file_ext,
	input             ioctl_wait,
```

## SDRAM board size

```Verilog
	// [15]: 0 - unset, 1 - set. [1:0]: 0 - none, 1 - 32MB, 2 - 64MB, 3 - 128MB
	// [14]: debug mode: [8]: 1 - phase up, 0 - phase down. [7:0]: amount of shift.
	output reg [15:0] sdram_sz,
```

## RTC



```Verilog
	// RTC MSM6242B layout
	output reg [64:0] RTC,

	// Seconds since 1970-01-01 00:00:00
	output reg [32:0] TIMESTAMP,
```

## UART Flags
```Verilog
	// UART flags
	output reg  [7:0] uart_mode,
	output reg [31:0] uart_speed,
```

## Keyboard emulation

The hps_io module has two ways of accessing the keyboard and mouse. It provides ps2 compatible signals which are useful for porting cores that are expecting a ps/2 keyboard. It also provides an easier to use more reliable interface.

To use the new interface, ps2_key[10] is toggled with each keypress. ps2_key[9] is whether the key is pressed or not. And the rest of the bits are pretty standard ps2 bits with bit 8 being the extended bit.



```Verilog
	// ps2 keyboard emulation
	output            ps2_kbd_clk_out,
	output            ps2_kbd_data_out,
	input             ps2_kbd_clk_in,
	input             ps2_kbd_data_in,

	input       [2:0] ps2_kbd_led_status,
	input       [2:0] ps2_kbd_led_use,

	output            ps2_mouse_clk_out,
	output            ps2_mouse_data_out,
	input             ps2_mouse_clk_in,
	input             ps2_mouse_data_in,

	// ps2 alternative interface.

	// [8] - extended, [9] - pressed, [10] - toggles with every press/release
	output reg [10:0] ps2_key = 0,

	// [24] - toggles with every event
	output reg [24:0] ps2_mouse = 0,
	output reg [15:0] ps2_mouse_ext = 0, // 15:8 - reserved(additional buttons), 7:0 - wheel movements
```
## Gamma 
```Verilog
	inout      [21:0] gamma_bus,
```

## ??
```Verilog
	// for core-specific extensions
	inout      [35:0] EXT_BUS
```