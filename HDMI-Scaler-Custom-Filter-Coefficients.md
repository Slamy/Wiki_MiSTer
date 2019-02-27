
## Introduction

In November 2018, a feature was added to MiSTer to allow the the video scaler to load filter coefficients for arbitrary interpolation filters.  This allows MiSTer to scale it's output over HDMI with common image scaling algorithms such as Bicubic as well as other scaling algorithms better suited for enlarging pixel graphics.  Additionally, some special effects such as scanlines and lcd effects can implemented through filter coefficients.

## How to use filter coeffcients

To use any of the pre-made filter coefficients (or your own) you need

* An updated version of MiSTer ([Main_MiSTer](https://github.com/MiSTer-devel/Main_MiSTer)).  The first release with support was MiSTer_20181116.
* A supported core.  Most cores released after November 16, 2018 have support for filter coefficients.  Nearly every core updated after Nov. 16 2018 supports custom scaler coefficients.  However many arcade cores have not been updated to the newest MiSTer /sys files yet.
* The best place to get a pack of working filters is to download the filter pack here: [Filters_20190216.zip](https://github.com/MiSTer-devel/Filters_MiSTer/tree/master/Releases).
* Place the Filters folder from the newest release's zip file onto you sd card. Technically you should also be able to place the zip file itself into the "Filters" folder on your sd card because newer versions of MiSTer support reading from zip files as if they were folders.

Once you have updated MiSTer and Cores and your filter coefficients in the right place you simply

* Start a supported core
* Go to page 2 of the core's OSD menu and under HDMI Scaler: change the option from "Filter - Internal" to "Filter - Custom"
* The option below "Filter - Custom" should now be enabled and will allow you to choose your filter from the files in your /Filters folder.

## Frequently Asked Questions
Q: What filter should I use?

A: It's up to you.  The "Gaussian_Sharp_05" filter is a good tradeoff between sharpness and shimmering during scrolling.  If you like scanline effects, try the "Normal_Scanlines_XX" filters.  To minimize artifacts from uneven scaling, I recommend that you set the `vscale_mode=2` in your mister.ini (this locks the scaler into 0.5x scale factors 4.0, 4.5, etc) and set the output resolution to your display's native resolution.  If you don't have a mister.ini, then start with the default file here: [MiSTer.ini](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/MiSTer.ini) and place this in your SD card /config folder.

Q: Why would I want to use custom filter coefficients?

A: There are many reasons. To get better/different quality than the internal scaler is the main reason. To use scanline or lcd effects is another.

Q: Doesn't MiSTer already have scanlines through the "Scandoubler FX" option in the OSD?

A: Yes, but the scanlines available with "Scandoubler FX" are aligned to the scandoubled image and the scanlines through the filter coefficients are aligned to the original pixels in the scanline.  So you achieve better scanlines with filter coefficients in most cases.

Q: How does this relate to the earlier "coeff.txt" support available in some cores or the "NN" builds that support nearest neighbor scaling?

A: The "NN" builds were hardcoded to perform Nearest Neighbor upscaling only.  Nearest Neighbor scaling is available as a set of filter coefficients.  The "coeff.txt" builds were the frst attempts by Sorgelig to implemment support for custom filter coefficients in MiSTer.  There was no support in the OSD for choosing the filter in these older builds.  These newer builds replace those older builds.

Q: Where do I get sets of Filter Coefficients?

A: The Filter Coefficients are on github here: [MiSTer Filter Coeffecients](https://github.com/MiSTer-devel/Filters_MiSTer)

## What do some filters look like?

Many filters exist already.  Here are samples of just a few:

Gaussian_Sharp_05: 

![Sharper Bilinear Filter](http://i63.tinypic.com/a29p8k.jpg)

Normal 30% Scanlines:

![Sharp Bilinear with 30% Scanlines](http://i63.tinypic.com/2s78847.jpg)

LCD Effect (no blur):

![LCD Effect](http://i67.tinypic.com/10px9ph.jpg)


## Technial Information

The VIP scaler implements a generic 4 tap, 16 phase polyphase filter.  Details are on page 189 of the VIP scaler docs here: [Intel VIP Scaler Doc](https://www.intel.com/content/dam/www/programmable/us/en/pdfs/literature/ug/ug_vip.pdf)

The Zipcores Application Notes pdf explains the workings of the filter much better than the ALtera/Intel docs: [Zipcores Application Notes](http://www.zipcores.com/datasheets/app_note_zc003.pdf)

Most of the currently available filter coefficients were generated with the Matlab code here: [Filter Coefficient Calculator Matlab Code](https://github.com/MiSTer-devel/Filters_MiSTer/tree/master/Matlab).

### Tips for understanding the MiSTer filter coefficient text files:

* There are separate coefficients for horizontal and vertical scaling.
* Each row of the Filter Text File list the coefficients for taps T0, T1, T2, T3 for a particular phase.
* The first row is phase 0 and corresponds to the center of tap T1.
* The ninth row is phase 8 and corresponds to the halfway point between T1 and T1 (so it's the pixel edge between T1 and T2).
* Then last row is phase 15 and corresponds to 15/16th of the way from T1 to T2 (so one phase before the center T2).

### Sample Coefficient Set. Note the following:

* This is a 2 tap filter because we only have non-zero coefficients for taps T1 and T2
* The vertical coefficients don't sum to 128 for the middle phases. Since they sum to less than 128, the output will be darker. That's how scanlines are implemented.

<pre>
# range -128..128
# sum of line must not exceed the range!

# Sharp Bilinear on x-axis and y-axis
# 40% Scanlines on y-axis

# horizontal coefficients
   0, 128,   0,   0
   0, 128,   0,   0
   0, 127,   1,   0
   0, 125,   3,   0
   0, 120,   8,   0
   0, 112,  16,   0
   0, 101,  27,   0
   0,  85,  43,   0
   0,  64,  64,   0
   0,  43,  85,   0
   0,  27, 101,   0
   0,  16, 112,   0
   0,   8, 120,   0
   0,   3, 125,   0
   0,   1, 127,   0
   0,   0, 128,   0

# vertical coefficients
   0, 128,   0,   0
   0, 126,   1,   0
   0, 116,   5,   0
   0, 102,  10,   0
   0,  86,  16,   0
   0,  71,  21,   0
   0,  57,  26,   0
   0,  46,  31,   0
   0,  38,  38,   0
   0,  31,  46,   0
   0,  26,  57,   0
   0,  21,  71,   0
   0,  16,  86,   0
   0,  10, 102,   0
   0,   5, 116,   0
   0,   1, 126,   0
</pre>
