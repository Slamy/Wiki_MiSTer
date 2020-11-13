This page contains commonly asked questions and their answers.

## Table of Contents
**General**
- [When will MiSTer support cartridges?](#when-will-mister-support-cartridges)
- [Does MiSTer have lag?](#does-mister-have-lag)
- [I've seen in the news, "Update Framework". What does that mean?](#ive-seen-in-the-news-update-framework--what-does-that-mean)

**Controllers**
- [Can I use original console controllers?](#can-i-use-original-console-controllers)
- [What about light guns?](#what-about-light-guns)
- [Any USB controller recommendations?](#any-usb-controller-recommendations)
- [What are the USB controller options?](#what-are-the-usb-controller-options)
- [Can I increase the polling rate of my USB controller to improve input latency?](h#can-i-increase-the-polling-rate-of-my-usb-controller-to-improve-input-latency)
- [Do I need the official USB Hub Add-On Board?](#do-i-need-the-official-usb-hub-add-on-board)
- [Do I need to have a USB keyboard with me to use MiSTer?](#do-i-need-to-have-a-usb-keyboard-with-me-to-use-mister)
- [How do I add a second controller to MiSTer?](#how-do-i-add-a-second-controller-to-mister)

**I/O Board**
- [Does MiSTer need an IO board?](#does-mister-need-an-io-board)
- [What are the methods for connecting controllers to the serial port of the IO add-on board?](#what-are-the-methods-for-connecting-controllers-to-the-serial-port-of-the-io-add-on-board)
- [Do I need an IO board to get analog video output to my CRT?](#do-i-need-an-io-board-to-get-analog-video-output-to-my-crt)


**Hardware**
- [Is MiSTer hard to set up? Is it really only for technical people who like to tinker?](#is-mister-hard-to-set-up--is-it-really-only-for-technical-people-who-like-to-tinker)
- [Which cores require SDRAM?](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Frequently-Asked-Questions#which-cores-require-sdram)
- [Why does NES core require RAM board when Genesis does not?](#why-does-nes-core-require-ram-board-when-genesis-does-not)
- [Does my MiSTer need cooling?](#does-my-mister-need-cooling)
- [What power supply is compatible with MiSTer / DE-10 Nano?](#what-power-supply-is-compatible-with-mister--de-10-nano)
- [My MiSTer needs a case. What should I do?](#my-mister-needs-a-case--what-should-i-do)
- [What kind of screws do I use with the DE-10 Nano's 14mm long brass standoffs?](#what-kind-of-screws-do-i-use-with-the-de-10-nanos-14mm-long-brass-standoffs)


**Video**
- [How do I set up MiSTer for 1080p, shimmer free gameplay?](#how-do-i-set-up-mister-for-1080p-shimmer-free-gameplay)
- [How do I get the scanlines filters on my MiSTer to look good?](#how-do-i-get-the-scanlines-filters-on-my-mister-to-look-good)
- [I have a 4k or other higher than 1080p display. Does MiSTer support that resolution? I'd like better video scaling.](#i-have-a-4k-or-other-higher-than-1080p-display--does-mister-support-that-resolution--id-like-to-enjoy-better-video-scaling)

**Cores**
- [How does the accuracy level of various MiSTer cores compare to other FPGA options?](#how-does-the-accuracy-level-of-various-mister-cores-compare-to-other-fpga-options)
- [Will any MiSTer core ever get save states?](#will-any-mister-core-ever-get-save-states)
- [Why doesn’t this core from another repo work? Why is MiSTer so hard to use?](#why-doesnt-this-core-from-another-repo-work-why-is-mister-so-hard-to-use)
- [When is N64 core coming?](#when-is-n64-core-coming)
- [When is PlayStation core coming?](#when-is-playstation-core-coming)
- [Other cores work but I get a black screen for this one. What do I do?](#other-cores-work-but-i-get-a-black-screen-for-this-one-what-do-i-do)
- [My CD games don’t work! Help!](#my-cd-games-dont-work-help)
- [What version of the CD card bios do I need for TG16 CD?](#what-version-of-the-cd-card-bios-do-i-need-for-tg16-cd)
- [How do I make MiSTer boot into the NES core in a specific game?](#how-do-i-make-mister-boot-into-the-nes-core-into-a-specific-game)

**Other**
- [I heard the DE10-Nano board uses subsidized components. Is MiSTer doomed if that stops?](#i-heard-the-de10-nano-board-uses-subsidized-components-is-mister-doomed-if-that-stops)
- [I see a defect that some other people aren’t seeing. Should I get a different de-10 nano?](#i-see-a-defect-that-some-other-people-arent-seeing-should-i-get-a-different-de-10-nano)
- [I found some other Cyclone based dev board on sale and it has built in WiFi. Can I use it for MiSTer?](#i-found-some-other-cyclone-based-dev-board-on-sale-and-it-has-built-in-wifi-can-i-use-it-for-mister)
- [The DE-10 is rated for up to 100°C operation and it doesn’t get nearly that hot. Do I really need a fan or heatsink?](#the-de-10-is-rated-for-up-to-100c-operation-and-it-doesnt-get-nearly-that-hot--do-i-really-need-a-fan-or-heatsink)

***

##  When will MiSTer support cartridges?

MiSTer will never use physical cartridges. 

Not only is it outside the scope of the project which aims to replace the need for having real hardware, it is physically very impractical/impossible given the number of GPIO pins available from the FPGA.

## Does MiSTer have lag?

It depends on your setup, but generally it ranges from imperceptibly low to around one frame of lag.  Zero latency is possible with certain equipment.

_Long answer:_ You may see some latency depending on your display, controller and settings. But they can all be tweaked to a large extent if that is important to you. If you use a CRT and native peripherals like an original console, you will experience no additional latency compared to it. [See here](lag-explained) for a more detailed explanation.


## I've seen in the news, "Update Framework".  What does that mean?

The framework are the common elements between all cores that handle things like IO, video scaling, etc.


***

## Can I use original console controllers?

Yes, there are many USB adapters for original console controllers. They can also be connected directly via the IO board as detailed below.

## What about light guns?

Light guns such as the NES Zapper are too timing sensitive to work over USB, but will work fine on supported cores via the IO board as detailed below. 

## Any USB controller recommendations?

Yes, please refer to [this page](Selecting-Input-Devices)

## What are the USB controller options?

Almost any controller that uses USB will work with MiSTer. You can also use a Bluetooth or 2.4ghz USB adapter for wireless. 
To reduce input latency USB may be overclocked which works with some controllers.
* [USB overclock instructions](https://github.com/MiSTer-devel/Main_MiSTer/wiki/lag-explained#input-lag)
* [USB controller performance data](https://docs.google.com/spreadsheets/d/1-3dIE-YI5f7Ct2qzDZZrcqRqFYCy1Y-8hjPw6PmmhE0)
* [USB DaemonBite](https://github.com/MickGyver/DaemonBite-Retro-Controllers-USB) (known fast controller adapters): 

## Can I increase the polling rate of my USB controller to improve input latency?

Yes you can, [see here](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Lag-Explained#input-lag).

## Do I need the official USB Hub Add-On Board?

No, but you will probably want some sort of inexpensive OTG hub at least.

_Long answer:_ The USB Hub Addon Board can be considered a luxury item.  An inexpensive OTG USB HUB from online markets will work fine for many people.  The advantage of the addon board is that it physically integrates very cleanly and safely with the DE10 and it has seven powered USB ports which is plenty for almost any user.  Users who want to use many or several power hungry USB devices will want to at least be sure to get a USB Hub that is externally powered so as not to overtax the DE10’s power circuitry.  Take care to pay attention to the DE10’s rather delicate OTG USB port.  Another advantage of the addon board is that it very securely attaches to this port.  Corded OTG Hub users will want to be careful that this port is not stressed by a sudden jerk or a slow steady pull.

## Do I need to have a USB keyboard with me to use MiSTer?

Yes, it's a good idea to always have a USB keyboard available as sometimes you will need to remap controllers especially for additional players.

## How do I add a second controller to MiSTer?

Before you can use a second controller in a core, you'll need to set it up in the main menu, with no core loaded.  Plug it into a USB port, then define it from the OSD in the main menu.  Now you can define it in the various cores' OSD menus.

***

## Does MiSTer need an IO board?

No. The IO board is optional, but offers features that could be important for some users.

_Long answer:_ an Input/Output (IO) device, its primary function is to provide a native (original hardware) video signal to CRT monitors with zero lag (see FAQ question above) and audio for devices via 3.5mm audio cable or optical (TOSLINK) output.  HDMI video and audio will continue to function when using these analog outputs, which is convenient for streaming or capturing gameplay footage. The Input part of the board refers to the serial port, which uses a connector of the USB 3.0 standard (but is not a true USB port and will not support regular USB devices).  See FAQ question above for more information on how you would use this part of the IO board.  There are other small features of the IO board that serve minor purposes; please see [this page](IO-Board) for more information about them.

## What are the methods for connecting controllers to the serial port of the IO add-on board?

SNAC (Serial Native Accessory Converter) is a standard adapter made for direct wiring. Each supporting core (SNES, Genesis, NES, and TG16) allows the original controllers for those specific consoles to work as originally wired with those cores only. See [this page](https://github.com/blue212/SNAC
) for details on SNAC.

## Do I need an IO board to get analog video output to my CRT?

_Short answer:_ No.  You can use an HDMI to VGA adapter to do it instead.

_Long answer:_ Use of an inexpensive HDMI to VGA adapter is supported in most cores through [Direct Video](Direct-Video). Search online and you will find many inexpensive options.

***

## Is MiSTer hard to set up?  Is it really only for technical people who like to tinker?

No and no, but those who enjoy tinkering can get a lot extra out of their MiSTer if they wish.

[in depth]:  The hardware only requires minimum setup to run (DE-10 Nano board + am HDMI TV).  Attaching a memory board to your DE-10 is very simple, and wlll allow you to use all cores.  On the software side, minimally, all that is need is to prepare an SD card from a windows PC by running a simple SD card preparation/installation program and, then putting this card into the DE-10.  Copying files for use with cores such as ROM can then be done trivially either by copying them into the SD card or transferring them via FTP/network share into your MiSTer.

For more detail on the set up process you can follow [this Setup Guide](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Setup-Guide)

## Which cores require SDRAM?

You can find the updated list at the [SDRAM Requirements by core](https://github.com/MiSTer-devel/Main_MiSTer/wiki/SDRAM-Requirement-by-cores) section

## Why does NES core require RAM board when Genesis does not?
"_The short answer on the NES is because it doesn't use RAM to store graphics (typically; some carts do, though).  At any given pixel, it can grab graphics data from the Charcter ROMs at any location, so you need the entire graphics ROM to be available within a pixel's time. Genesis has graphics RAM and stores its data there (it's copied from the ROM).  The graphics RAM for Genesis is put in the core where it can be grabbed very quickly, so it doesn't matter if the CPU was slowed down for very small amounts when it was copied there.  The NES can't count on that small delay not causing issues when it reads the graphics data._" (GreyRogue)


## Does my MiSTer need cooling?

Yes, you will want at least a heatsink (passive cooling). 

_Long answer:_ While it's fine for general operations, the DE-10 board’s FPGA chip ideally requires a passive heatsink to avoid heat interfering with some of the more complex cores.  22mm x 22mm is the ideal heatsink size for this.  Active cooling (a fan) is recommended for long term use.  Some cores may present corruption/artifacts if the chip is not cooled with a fan.  A 40mm diameter fan, powered from either the IO board or directly from one of the DE-10’s GPIO pins, is the recommended type for this task.  Typically this fan is mounted on the optional IO board, however it can also be mounted on a 3D-printed plate or hand-cut piece of plastic or cardboard if you do not need or have an IO board.


## What power supply is compatible with MiSTer / DE-10 Nano?

The DE10 boards needs a 5V power supply with at least 2A. One such PSU is included with the DE10-Nano board.
The connector is a coaxial "barrel" plug of 5.5 mm outer diameter and 2.1 mm inner diameter, center positive.


## My MiSTer needs a case.  What should I do?

There are two routes you can take:  either make it yourself or purchase a case from an online vendor.  For purchasing the most popular cases are the Official (PCB) Case or the 3D printed case.  In DiY, various users have made custom cases out of metal, acrylic and/or wood, but the most popular method is to 3D print an enclosure.  You can find the necessary 3D print files online (e.g. thingiverse).

## What kind of screws do I use with the DE-10 Nano's 14mm long brass standoffs?

M3 screws, 8mm is a good length.


***

## How do I set up MiSTer for 1080p, shimmer free gameplay?

Set your device to 1080p60 by editing mister.ini on your SD card.  Search it for:  video_mode and change it to video_mode=8.  For shimmer free gaming, you’ll need to use a filter in each core. To do this, press your OSD button, flip right, and go to filters and select Interpolation (Sharp).  If you do not have anything in your filters folder, you can [download Interpolation sharp here](https://raw.githubusercontent.com/MiSTer-devel/Filters_MiSTer/master/Filters/Interpolation%20(Sharp).txt).  Put it in your ‘filters’ folder and select it and you’re good to go.

##  How do I get the scanlines filters on my MiSTer to look good?

In order for scanlines to look "perfect" on your flat panel display, you will need to set the device to integer scaling.  Do this by editing mister.ini on your SD card.  Search it for:  vscale_mode  and change it to vscale_mode=1.  Note, with integer scaling it's highly likely the core will not fill up the entire display, you will have black borders.  You can mitigate this by changing your vscale mode to 0, 2 or 3, but the scanlines will not be perfect; it is a compromise.

##  I have a 4k or other higher than 1080p display.  Does MiSTer support that resolution?  I'd like to enjoy better video scaling.

MiSTer can't quite reach 4k.  The current hardware limited maximum vertical resolution is 1536p.  You can set your resolution by editing mister.ini on your SD card, video_mode=12 for 1440p or video_mode=13 for 1536p.


***

## How does the accuracy level of various MiSTer cores compare to other FPGA options?

Most MiSTer cores are just as, if not more accurate, as any of the other major FPGA offerings available today.
[In depth]:  Most MiSTer cores are very mature at this point.  Generally accuracy is already so great that most people would not able to tell the difference between these cores and the original hardware.  Other FPGA options such as commercial clone consoles or various flash carts, are likewise extremely accurate. 

For more detail on exact status, please refer to the core's individual bug trackers. You can find the repository links from [this page](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Core-Status)

## Will any MiSTer core ever get save states?

The GBA core supports save states, but is the only one right now.

Save state are a complicated problem, specifically on an FPGA based systems. Cores need to be written from scratch to support them, as was done with the GBA core. At this time there are no plan to apply this to other cores, but it may happen one day.

## Why doesn’t this core from another repo work? Why is MiSTer so hard to use?

MiSTer repo is self contained and the updater only fetches from there. Cores on other repos are not fully integrated so results vary. 
Some developers have their own discord servers or forums and you can seek support there.


## When is N64 core coming?

Probably never. There isn’t really sufficient bandwidth.

## When is PlayStation core coming?

Probably next year. Serious progress has been made by a few developers but there’s no official ETA.


##  Other cores work but I get a black screen for this one. What do I do?

Try setting vsync to 0 as your display may not support all refresh rates. (Note that this was the default setting.)

## My CD games don’t work! Help!

Unzip them. Do not zip CD games. Also put them in iso/wav/bin/img + cue format.

## What version of the CD card bios do I need for TG16 CD?
Use Japanese version 3.0. You will commonly find it with filename:
Super CD-ROM System (Japan) (v3.0).pce

## How do I make MisTer boot into the NES core into a specific game?
You need to use two different options: autobooting a core, and starting the core on a given ROM. Here is how:
In the .INI file, set `bootcore=NES_20201102.rbf` (or the specific core version you have), and comment out `;bootcore_timeout`.
Then on your NES games folder (e.g. `/media/fat/games/NES/`, copy the FDS bios as `boot0.rom`, and your .NES rom to boot as `boot1.rom`.
For more options, please refer to the [NES core documentation](https://github.com/MiSTer-devel/NES_MiSTer#installation) 


***


## I heard the DE10-Nano board uses subsidized components. Is MiSTer doomed if that stops?

The DE10 Nano is broadly sold to universities and is available in larger supply than custom hardware made only for retro enthusiasts. In general, these development boards are manufactured and sold for a long time (the last generation DE1 board is still sold), so there is no reason to be concerned. Worst case, the work done in cores can be ported to other boards in the future. For now, the DE10-Nano remains the best and most cost-effective option, and MiSTer is a perfect fit for it as the boards are intended to introduce FPGA programming to a wider audience.

## I see a defect that some other people aren’t seeing. Should I get a different DE-10 Nano?

No, you should report the defect and wait for a fix. There is no magical best DE-10 Nano.

##  I found some other Cyclone based dev board on sale and it has built in WiFi. Can I use it for MiSTer?

Generally, no. While it’s always possible that someone will take time to port things to other boards, the different pins and memory will mean it won’t be a straight use and unless it’s a significant upgrade, it would never gain official support.

## The DE-10 is rated for up to 100°C operation and it doesn’t get nearly that hot.  Do I really need a fan or heatsink? 

While 100°C is where the chips may begin to become damaged, high heat impacts more than just the health of the chip.  On FPGA's, core stability can also be altered by temperature, so a number of cores with difficulty with timings, like AO486 for example, benefit from having the chip at cooler temperatures.


