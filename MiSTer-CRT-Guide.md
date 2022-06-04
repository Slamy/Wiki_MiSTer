MiSTer FPGA project, while mainly  focused on HDMI output, is at the moment also the best all-in-one emulation solution for displaying [old consoles and microcomputers on CRT sets](https://docs.google.com/spreadsheets/d/1-Le6cJ0Fzxgo3pglolequL6Fq1WynjaPWTT_jkZlBbI/edit#gid=1304126374). Most of MiSTer's cores should output image representing the original sources 1:1 natively and with few adjustments necessary.

The whole subject is quite vast though, seeing as CRT hardware can be quite varied and cause compatibility issues. Also, different cores might output the signal in different ways, or still have some bugs present. This wiki is an attempt to consolidate the current knowledge regarding this topic and present it in a concise manner, while also serving as a first-stop resource for solving assorted problems. 

As of March 2022 this guide is still considered work-in-progress, seeing we've only just started writing it, and MiSTer itself is constantly evolving - cores are being improved and new solutions appear. **If you spot any mistakes and/or can contribute something new you are welcome to edit this wiki**. Please try to let us know on the [forums](https://misterfpga.org/viewtopic.php?t=4373) or [Discord](https://discord.com/invite/misterfpga) though, so we can cross-check the new information and learn about it too.

Some disclaimers:  
-all (ok, 99.73%) of the settings/solutions here have been tested and proven working, but they still might not work on your setup. There are many quirky situations possible in the CRT world.  
-Before buying something (cable, adapter, etc) make sure you read sellers' product description and double check it is applicable in your particular scenario.  

### Table of contents
[1. CONNECTING TO RGB / COMPONENT / VGA capable sets](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#connecting-to-rgb--component--vga-capable-sets)  
[2. CONNECTING TO COMPOSITE / S-VIDEO capable sets](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#connecting-to-composite--s-video)  
[3. MISTER INI SETTINGS](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#misterini-settings)  
[4. CORE OSD SETTINGS](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#core-osd-settings)  
[5. CUSTOM VIDEO MODES](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#custom-video-modes)  
[6. F.A.Q.](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#faq)  
[7. REMAINING CORE PROBLEMS](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#remaining-core-problems)


## CONNECTING TO RGB / COMPONENT / VGA capable sets

### BOARDS / CONVERTERS
You can connect MiSTer to a CRT set using two methods: either by installing the analogue I/O board and using its VGA output or by connecting an HDMI-to-VGA DAC dongle directly to DE10 Nano's HDMI socket. Both of these methods produce nearly identical image which in most cases should match the output of the original hardware 1:1. Apart from that, they also have their specific pros & cons:

* Analogue I/O board
  * **Pros**: extra features (buttons, led lights, etc), doesn't need SoG mod to connect to component 
  * **Cons**: more expensive, lesser colour depth in some cores, can't use 2xSDRAM, lower quality sound output

* Direct Video
  * **Pros**: better colour depth, much cheaper, does not block 2xSDRAM, better audio
  * **Cons**: no extra features, needs extra modification for component, not all the dongles are guaranteed to work, needs VGA2SCART adapter to handle modelines  

Once you have acquired either an I/O board or a DV dongle, you'll need to connect it to your TV via a cable and also change some settings in the mister.ini file.

### CABLES 

* for consumer TVs (15kHz) with RGB SCART (via both I/O board & Direct Video)     
Apart  from I/O board or Direct Video dongle you'll also need a special cable. You can either make one [LINK] or buy it online. [It's recommended](https://www.retrorgb.com/beware-of-mister-scart-cables.html) to get a cable with a 470 ohm resistor on the Composite Sync line (best ask the seller if it already has one)    
  
    Here are some possible sources: [Misteraddons (US)](https://misteraddons.com/collections/parts/products/video-cables-hdmi-scart-ypbpr), [Retro Access (UK)](https://retro-access.com/products/mister-io-scart?_pos=1&_sid=97cb11000&_ss=r), [Ultimatemister (PT)](https://ultimatemister.com/product/rgb-scart-cable/), [Wolfsoft (DE)](https://www.wolfsoft.de/shop/product_info.php/products_id/15401//mister-premium-rgb-kabel-2m.html), [Antoniovillena (ES)](https://www.antoniovillena.es/store/product/vga-scart-cable/). 
You can also get a MiST cable, it works in general but might be lacking the 470 Ohm resistor and is generally "not guaranteed":  [Lotharek (PL)](https://lotharek.pl/productdetail.php?id=171), [Amigastore (EU)](http://amigastore.eu/en/512-mist-scart-cable-mist-db15-f-to-scart-tv.html)
Other option is to use a VGA-SCART converter, plus normal SCART/VGA cables. Possible sources:  [Antoniovillena (ES)](https://www.antoniovillena.es/store/product/vga-scart-adapter/), [Arcadeforge (DE)](https://arcadeforge.net/UMSA/UMSA-Ultimate-SCART-Adapter::57.html?language=en), [Retro Upgrades (UK)](https://www.retroupgrades.co.uk/product/vga2scart/)

    If you are connecting to a consumer Trinitron you might also need to add an extra resistor/potentiometer to fix odd or not lively enough colours  [forum link](https://misterfpga.org/viewtopic.php?p=4162#p4162)   
As of May 2022 the [Ultimatemister shop](https://ultimatemister.com/product/scart-rgb-to-1084-db9/) sells all-in-one Direct Video cables (HDMI to SCART) which eliminate the need for a Direct Video adapter. 

* consumer TVs (15kHz) with YPbPr component (via I/O board)  
A standard VGA to Component cable should be enough

* consumer TVs (15kHz) with YPbPr component (via Direct Video)   
This will require cable modifications, to add Sync on Green (SoG). Please read more here: [Wiki](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Direct-Video#setup-for-ypbpr-signals) / [forum](https://misterfpga.org/viewtopic.php?f=33&t=1471)

* VGA monitors (31Khz)
A standard VGA – VGA cable should be enough.

* PVM/BVM monitors (via I/O board)  
A standard VGA to BNC cable (3xRGB + HSync) cable should be ok 

* PVM/BVM monitors (via Direct Video)  
A standard VGA to BNC cable (3xRGB + HSync) cable should be ok
* Commodore monitors  
Cable for 1084S monitor is sold by [Ultimatemister (PT)](https://ultimatemister.com/product/mister-commodore-1084s/)

### SETTINGS
Most of the settings' changes are done in mister.ini, located in the  “media/fat/” directory of your SD card. When troubleshooting it is advised to use a new mister.ini from [this link](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/MiSTer.ini). All .ini settings in this section assume you are using this default file. 

**For I/O BOARD**  
* consumer TVs (15kHz) with RGB SCART  
 `composite_sync=1`

* consumer TVs (15kHz) with Component  
  `ypbpr=1`  
 Also you might need to flip the SoG switch on the I/O board  
 
* VGA monitors (31khz)  
 `forced_scandoubler=1`

**For DIRECT VIDEO**
* consumer TVs (15kHz) with RGB SCART   
`direct_video=1  `  
`composite_sync=1`

* consumer TVs (15kHz) with Component    
`direct_video=1  `  
`composite_sync=1`  
`ypbpr=1` 

* VGA monitors (31khz)  
`direct_video=1  `  
`forced_scandoubler=1`

* for PVM/BVM monitors  
`direct_video=1  `  
`composite_sync=1`

## CONNECTING TO COMPOSITE / S-VIDEO 
One method of obtaining Composite or S-Video on a capable CRT TV set is by using a special adapter. At the moment these are available for sale from [Antoniovillena](https://www.antoniovillena.es/store/product/vga-composite-s-video-adapter/) and [Ultimatemister (PT)](https://ultimatemister.com/product/mister-vga-to-composite-s-video/)  

There's also an open-source design which you can DIY: [Github](https://github.com/MikeS11/MiSTerCRT) / [forum link](https://misterfpga.org/viewtopic.php?f=33&t=2894).  

**These adapters have been reported to work well in S-Video mode, but Composite has problems with artifacting.**  

Another alternative is the [Axunworks converter](https://www.axunworks.com/RGB-to-Composite-S-Video-p341706.html). It requires using a VGA-to-BNC cable with BNC-to-RCA adapters and most likely also suffers from artifacting in Composite [(forum thread)](https://shmups.system11.org/viewtopic.php?f=6&t=63452&start=270). Some other options reported to work well are converters from seller "wakabavideo" and "Keene Scart to S-Video" brand on ebay.  

### Custom YC (S-Video / Composite) Cores
These requirements are for cores that natively output s-video / composite directly from the core. The current cores generate two signals that use the existing RGB pins, where the luma (Brightness) uses the green output and the chroma (Color) uses the red output.

**Connection Requirements - S-Video**
- A custom breakout board / cable  the converts VGA to S-Video
- VGA to Component Cable (Only requirement for some monitors, i.e Commodore 1702)
- Custom RCA to S-Video Connector

**Connection Requirements - Composite**
- A custom breakout board / cable the converts VGA to Composite
- VGA to Component Cable to a 1-Male to 2-Female RCA Y-Adapter Splitter Cable

*Note 1: Its recommended that you use a 0.47nF Capacitor in series with the Chroma signal. This will reduce the output voltage of your composite signal.*    
*Note 2: If using composite, it is recommended to use a breakout board with a luma trap that will filter out frequencies that confuse the tv from thinking brightness changes are color. (E.g Color Bleed / Rainbowing)*

#### Using an Analog IO Board
**Configuration Requirements**

- Sync on Green - ON
- Enable S-Video in the core menu

**INI Settings**   
`vga_scaler=0`   

#### Using Direct Video
**Configuration Requirements**   
- A Sync On Green Circuit is Required. Please read more here: [Wiki](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Direct-Video#setup-for-ypbpr-signals "Wiki")
- Enable S-Video in the core menu

**INI Settings**   
`YPbPr = 0`   
`Direct_video = 1`   
`Composite sync = 1`   
`vga_scaler=0`   
  
More info & updates: [Twitter](https://twitter.com/MikeSimone3) / [Github](https://github.com/MikeS11/Test_Pattern_YC) / [forum](https://misterfpga.org/viewtopic.php?t=4434)

## MISTER.INI SETTINGS
Listed here are some other mister.ini settings which might be useful when dealing with CRTs. Mister.ini can be found in the "media/fat/"directory of your SD card. Please refer to the linked Wiki pages for their parameters and more details.

[`[core name]`](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Configuration-Files#adding-core-specific-settings) – eg [ao486]
Useful for setting core-specific variables. Any settings below these tags will ignore the ones under the main [mister] tag. Not needed in most cases. Put at the end of mister.ini

[`hdmi_limited`](https://github.com/MiSTer-devel/Main_MiSTer/wiki/Configuration-Files#hdmi_limited) - used for Direct Video, when there's a possibility that your adapter  might have a limited colour range.


`vsync_adjust`,`vga_scaler`, `vscale_mode`, `video_mode` - these settings are ignored by the native analog output, and used only when the scaler is active. See [Custom Video Modes](https://github.com/MiSTer-devel/Main_MiSTer/wiki/_new#custom-video-modes)

## CORE OSD SETTINGS 
*This section needs expanding.*  
MiSTer's OSD Menu (F12 from keyboard or user-defined key on gamepad) contains two types of video settings: core specific and global. The former (if available) are in the "core_name" tab, the latter are under "Video Processing" in the "System" tab (press Right after evoking the Menu).  

The **core-specific Video settings** can vary from platform to platform and sometimes have effect on CRT use. There are also some settings which are the same across most of the cores, but they seldom affect the analogue output (eg `Vertical Crop`). The following ones are worth noting:  
`Aspect ratio`,`Scale` - useful when using custom modelines, sometimes necessary to achieve full screen and/or proper aspect ratio  
`Scandoubler Fx` - beware of accidentially setting it "on" when using 15kHz CRTs. This  will cause the image to go out of sync and might seem as if something is "broken".  

The **global Video settings** from Video Processing are mostly dedicated to HDMI users, dealing with various image filters. CRT users can however also try and apply the `Gamma Correction` filters here.  

## CUSTOM VIDEO MODES
**Using custom modelines carries a small risk of damaging your set. Most CRT TVs and monitors, especially the newer ones, should be fine with out-of-spec signals, but the possibility of something going wrong remains, so use them at your own risk.**


While most of MiSTer's cores work very well with CRTs natively, and display the same image as original hardware, there are some cases when using custom modelines might be beneficial. For example, displaying 31kHz cores on 15kHz sets, or slightly adjusting output of cores such as NeoGeo.
These modelines have to be calculated individually and entered in mister.ini after a core-specific tag (eg [ao486]) using `video_mode` setting.

Please note that when using them, you might also need to correct some of the cores' video-related OSD settings. Usually it's `Aspect Ratio` and/or `Scaling` that needs adjusting. Also, they won't work with Direct Video, for that you'd need to add a device/mod with HV Sync combiner, like one of the VGA2SCART adapters [mentioned above.](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide#cables)

### CRT MODELINE HOW-TO
For more information on how to create custom modelines please refer to [Thorr's CRT modeline creation guide](https://github.com/MiSTer-devel/Main_MiSTer/wiki/THORR%E2%80%99S-CRT-MODELINE-CREATION-GUIDE), as well as [Shogun's forum thread](https://misterfpga.org/viewtopic.php?t=3249).  

### EXAMPLE MODELINES
Below are modelines which have been tested and confirmed to be working. That does not mean that they necessarily will work on your set though. If a modeline does not work you can try another one, if there are available alternatives, and if not, try to make one yourself or adjust the existing ones by using the [calculators](https://misterfpga.org/viewtopic.php?t=3249). You can also experiment with `vsync_adjust` in  such cases.

In case when an example contains multiple video_modes, you can try different ones by removing/adding ";" from the front of the line. Only one video_mode can be active at a time, so the ";" is used to disable the unwanted ones (this can be applied to all the settings in the mister.ini)

Settings provided here assume that you have already applied the necessary ones from the initial paragraphs and that you are able to display most of the cores correctly. Please also note that when using them, **you might also need to correct some of the cores' video-related OSD settings**. Usually it's `Aspect Ratio` and/or `Scaling` that needs adjusting.

### ao486  
This core natively outputs 31kHz (although not without problems) and so is meant to be used on VGA monitors, but it's possible to display it on consumer sets too, using modelines. There will be some black borders, and the MSDOS text only just about readable, but the 320x200 games should be scaled perfectly.

-for 15kHz sets  
`[ao486]`  
`direct_video=0`  
`vscale_border=20`  
`vscale_mode=0`  
`;video_mode=1440,40,136,176,240,3,10,6,27000`  

-for 15kHz sets  - another example. If you have the previous one in your config, remember to disable it using ";".  
`[ao486]`  
`direct_video=0`  
`vga_scaler=1`  
`vsync_adjust=1`  
`vscale_mode=1 ; Set this to 0 if you want to fill the screen but lose 1 to 1 pixel mapping on 320x200 games`  
`;video_mode=1280,170,140,244,240,2,0,22,29020`  
`;video_mode=1280,138,140,216,240,2,0,22,28070`  
`video_mode=1280,120,140,202,240,2,0,22,27565; Wider`  

More modelines and discussion are [in this thread](https://misterfpga.org/viewtopic.php?t=2574&start=30)  

-for 31kHz VGA monitors - As of March 2022 there's a new method of dealing with [mode changing](https://misterfpga.org/viewtopic.php?p=44771#p44771)  It can be used for all the cores, but so far has the biggest application in ao486, allowing for automatic resolution switching between DOS and a variety of  games with different parameters. You can also choose to apply the CGA/EGA era "look" with pronounced scanlines.  

`[ao486]`  
`; Set it to "Variable" in the video settings in the menu of the core`  
`video_mode=1600,64,192,304,1200,1,3,46,162000; This is the "catch-all" resolution that will be used if an undefined video mode is detected. This example may be too high of a resolution for your monitor. You can use video_mode=1 instead for example.`  
`direct_video=0 ; use the scaler`  
`vsync_adjust=2 ; minimal lag`  
`vscale_mode=1 ; integer scaling`  
`video_info=3 ; show resolution information for X seconds`  
`hdmi_limited=2 ; 1 - use limited (16..235) color range over HDMI  ; 2 - use limited (16..255) color range over HDMI, for VGA converters.`  

`[video=320x200@70.1]`  
`;video_mode=320,24,49,38,200,2,2,20,13535,0,1 ; 320x200@140.2Hz@31.4kHz DOS CGA/EGA/Adventure games with scanlines`  
`video_mode=640,7,108,30,400,13,2,34,24708,0,1 ; 640x400@70.1Hz@31.48kHz VGA era games including 320x200, 320x400, 640x400 @70.1Hz`  
`[video=320x400@70.1]`   
`video_mode=640,7,108,30,400,13,2,34,24708,0,1 ; 640x400@70.1Hz@31.48kHz VGA Games including 320x200, 320x400, 640x400 @70.1Hz`  
`[video=720x400@70.1]`  
`video_mode=720,15,108,46,400,13,2,34,27983,0,1 ; 720x400@70.1Hz@31.48kHz DOS Text`  
`;experimental modes`  
`[video=320x199@59.7]`  
`video_mode=640,25,130,75,398,50,29,50,27370,0,1 ; 640x398@59.7Hz@31.46kHz Jazz Jackrabbit`  
`[video=320x240@59.7]`  
`video_mode=640,40,96,64,480,14,2,31,26430,0,1 ; 640x480@59.7Hz Epic Pinball (temp modeline, still under development)`  
`[video=640x480@59.7]`  
`video_mode=640,40,96,64,480,14,2,31,26430,0,1 ; 640x480@59.7Hz (temp modeline, still under development)`  
 
### NeoGeo 

-for 15kHz sets - these modelines can help with horizontal scaling  
`[NeoGeo]`  
`direct_video=0`  
`vga_scaler=1`  
`;video_mode=320,7,28,29,224,16,8,16,6000`  
`video_mode=320,21,29,44,224,13,14,13,6400`  

[Forum thread](https://misterfpga.org/viewtopic.php?t=3238)  

### PC-8801  
This early Japanese computer was able to output 15kHz (tbc) but the core at the moment only outputs 31kHz. Using these modelines you should also experiment with V-modes in the core's OSD options.  

-for 15kHz sets  
`[PC8801]`  
`direct_video=0`  
`vga_scaler=1`  
`vsync_adjust=2`  
`vscale_mode=3`  
`video_mode=1280,159,140,248,240,11,0,19,29568 ; Good for 320x200 games, not 320x240`  
`;video_mode=1280,173,140,266,240,11,0,19,30086 ; slightly bigger borders on left and right`  

### RX-78  
This modeline helps to center the image.  

-for 15kHz sets  
`[RX78]`  
`direct_video=0`  
`vga_scaler=1`  
`video_mode=640,6,56,66,224,14,8,18,12000`  

### X68000 
X68000 is one of the most complex machines when it comes to output, sporting three different frequencies and a host of resolutions. MiSTer's core outputs 31kHz, it is however possible to display at least some games with 1:1 scaling (and maybe a little overscan) on 15kHz sets. Please [check this thread](https://misterfpga.org/viewtopic.php?f=36&t=3624) for more modelines and explanations.  

-for 15 kHz sets  
`[X68000]`  
`vga_scaler=1`  
`vsync_adjust=1`  
`vscale_mode=0`  
`vscale_border=0`  
`video_mode=1024,116,72,160,256,1,1,3,20400`  

### MiSTer Menu
At the moment MiSTer's text displayed while updating is cut off a bit - this modeline fixes it.  

-for 15kHz sets  
`[Menu]`  
`direct_video=0`  
`vga_scaler=1`  
`vsync_adjust=1`  
`vscale_mode=1`  
`video_mode=640,54,56,106,224,16,0,28,13764`  

## F.A.Q.  
This section is being continuously expanded and contains various CRT-related questions, solutions, hacks, etc...  

### Strange / faded colours on some Trinitron sets
Some consumer Sony Trinitron TV's (perhaps also studio monitors) might struggle with more than 300mV of the sync level and need a resistor on the sync line. Using a 1k resistor (or 2k potentiometer for more flexibility) should solve this problem.    

  Forum thread [link](https://misterfpga.org/viewtopic.php?t=614) / [link](https://www.atari-forum.com/viewtopic.php?t=35515&sid=4d7b331d45b9787bebc8bae491167457)  

### 240p@120Hz on VGA monitors
Using modelines it is possible to display 240p content in 120Hz on VGA monitors. This produces a brighter image with more defined scanlines. The downsides are black bars and blurry motion.  

Forum thread: [link](https://misterfpga.org/viewtopic.php?t=3677)  
Mister.ini settings: 

`video_mode=2048,40,442,200,240,3,10,8,85909`  
`vga_scaler=1`  
`vscale_mode=1`  
`vsync_adjust=0`  

### MiSTer cores' 15kHz compatibility
There's a page on this wiki regarding this subject, but at the moment (April 2022) it's quite outdated. User NML32 is maintaining an [external doc](https://docs.google.com/spreadsheets/d/1-Le6cJ0Fzxgo3pglolequL6Fq1WynjaPWTT_jkZlBbI/edit#gid=1304126374) though. It's quite extensive and up to date.      



## REMAINING CORE PROBLEMS  
Official cores listed in this section should be able in theory to output 15 kHz signal, but at the moment (04-2022) are either unable to do so or have some problems. This will hopefully change in the future.  

* Alice MC10 - known bug, which will be fixed eventually  
* Acorn Archimedes - in the latest version image is corrupted in Full Screen. Version 201101 works ok.  
* BBC Micro - problems with Component output? Also, possible problems with multi-resolution games.  
* Galaxija  
* Orao  
* PC-88 - no native 15kHz at the moment but it's possible to use modelines to display at least some games properly. See [Custom Video Modes/PC-88](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide/_edit#pc-8801) section  
* X68000 similar to PC-88, see [Custom Video Modes/X68000](https://github.com/MiSTer-devel/Main_MiSTer/wiki/MiSTer-CRT-Guide/_edit#x68000) section  
* (to be confirmed) - the image on VGA monitors might be possibly dimmer via I/O board. [forum thread](https://misterfpga.org/viewtopic.php?p=2274#p2274)



