A common concern among retro enthusiasts is whether a device of this sort has _lag_ and whether it will create a less desirable experience compared to original hardware. 

Every electronic equipment exhibits some kind of _latency_, but it only becomes problematic if this latency causes frames to be missed. A frame is typically 16ms for a system using a 60 frames per second display (i.e. 1/60).

Lag is only problematic in a few specific cases:
* Some older games were designed to rely on extremely quick response (e.g. Punch Out on NES).
* If the latency is different between two players, it could introduce an unfair advantage.
* Lag that isn't constant can be an issue on games that require precise movement (most players usually adapts to constant lag).

There are three major categories of lag. Input, which involves controllers, mouse, etc, Processing, which would involve buffering in the core, execution or delays in code, and Display which involves the output of the video to your display device.

For a more detailed overview of lag and exploration of it, please refer to this page:
https://inputlag.science/

### Input
For input, MiSTer primarily uses USB. The latency of USB depends upon the controller itself, with most higher quality controllers predictably having lower latency. Initial tests indicate that some higher quality USB controllers will only take one or two milliseconds for the core to react. This is extremely dependant on the controller you use, and can’t be quantified as a single number because of this, however the USB stack is performant enough to have 1ms latency which should prevent lag in any noticeable form.

### Processing
This is one core advantage of emulation using FPGAs. Unlike software emulators which go through a cycle of executing, and then waiting for a screen refresh, FPGA cores run in real time, as the original hardware did. This means that cores don’t have CPU bottlenecks to slow them down arbitrarily or require additional large buffers to hold data under most circumstances.

### Display
MiSTer’s two primary display outputs are analog and HDMI. 

The analog output is driven as the original system would have, with no buffering, and so it will be effectively identical to the latency of a real console. From this point of view, the analog output cannot have any form of lag. 

When using HDMI output the image must be scaled up to fit the higher resolutions, which requires additional processing. The MiSTer scaler has options which impact its latency. vsync_adjust=2 in the ini file will result in about 4 scanlines of latency, while 0 or 1 will result in about 2 frames of latency, while having the advantage of being more compatible with displays. 

In addition your own television may introduce more latency, but this varies by device and no definite number can be given on that here. 

So in summary, if lag is critical to you, the best is to use a recommended USB controller tested by many and a CRT.
But even using an HDMI will result in a better experience than many other devices.

## Video options for HDMI

MiSTer offers options in how to configure its HDMI upscaler, making a tradeoff between compatibility and low latency.
These can be set in the MiSTER.INI file at the root of the SD card:

* vsync_adjust=2 is the best option if it is compatible with your TV
* vsync_adjust=1 is the second best option, but it adds 2 frames of latency
* vsync_adjust=0 is the lesser option, but the most compatible. 2 frames of latency and less smooth scrolling.

Long story short, vsync 0 guarantees 60hz output with an NTSC standard pixel clock, vsync 1 uses a framebuffer but is kept into original vsync (technically, varies the pixel clock per core), and vsync 2 has the original refresh rate and pixel clock of the core (no latency).