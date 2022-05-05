To create a custom modeline, first you need to know what your primary goal is and the limitations and/or desired features associated with that goal.  The goal will determine the parameters that you need to adhere to in order to come up with a good modeline.  A common goal is to try to match the vertical sync frequency to the source's original vertical sync frequency so there is no tearing.  

If your goal is to make a core work on a standard CRT TV, then you need to make sure the modeline falls within the acceptable range of frequencies that a TV can use.  You may not be able to match the vertical sync frequency on a CRT TV if the source frequency is not near 60Hz.  

If your goal is to have perfectly synchronized custom modes for ao486 on a VGA monitor or PVM, then your goal is to match the refresh rate and resolution or an integer scaled resolution of the source video mode. For lower resolutions such as 320x200@70.1Hz, a VGA monitor can't handle this without either doubling the refresh rate or doubling the vertical resolution.  Either option will work but look different.  

Doubling the refresh rate will give you thicker black scanlines and a more vivid image.  This could be great for having that TV look (especially for TV cores like arcade and NES cores) on a VGA monitor rather than using the forced_scandoubler setting in the MiSTer.ini.  

Doubling the vertical resolution will fill in the scanlines and make the image look smoother.  Back in the day, doubling the resolution was what was used on VGA monitors. Like with a CRT TV, you need to get the frequencies to be within acceptable ranges that the monitor can handle.  

The vertical resolution is much more important to pay attention to than the horizontal resolution.  You can safely double the horizontal resolution and it will effectively be no different than not doubling it as far as the electron beam is concerned when using integer scaling. However, doubling the vertical resolution will half the black area of the scanlines which may or may not be a desirable effect.  

## For VGA Monitors / PVMs (31kHz)  

Here is a walkthrough example of the steps that can be taken to try to get an ao486 mode of 640x480@59.7Hz that can be used for 320x240 games at the same vertical sync frequency.  

* First go to: http://xtiming.sourceforge.net/cgi-bin/xtiming.pl  
* Plug in 640 x 480 pixels
* Plug in 59.7 Hz
- Plug in 4 / 3 in the Constrain Aspect Ratio section
- Calculate the Modeline. It comes out to 'Modeline "640x480@59" 23.97 640 672 760 792 480 490 495 505'.
- Copy and Paste the Modeline into https://www.epanorama.net/faq/vga2rgb/calc.html
- Click Import Modeline
- Fix the Vertical Resolution box so it says 480 instead of 480@59
- Hit the Calculate button
- Look at the View calculated results section
- The Horizontal sync frequency needs to be within the range of the VGA monitor (anything around 30kHz and above is usually ok).  If the number is way above this, it may be to high for the monitor.  The higher the resolution and refresh rate, the higher this number may end up being.  If the number looks acceptable, it probably is.
- The Vertical sync frequency we want to have is 59.7Hz (because the game in ao486 told us this when we tried playing it and the video_info=5 was set in the MiSTer.ini). In this example, it says 59.93 so it is too high.
- In order to adjust the Vertical sync frequency, you can start by adjusting the Pixel clock frequency. It can handle three decimal places.  In this example, it says 23.97.  Try typing a new number that is lower, like 23.965, click Calculate and see what the new Vertical sync frequency is now.  In this example it is now 59.92.  Keep adjusting the number until you get 59.7.  Adjust the third decimal place so it is the lowest number that shows 59.7.  This is so it won't be 59.71 through 59.74 while showing 59.7 in the website.  The number that works in this example is 23.876.
- Now you have your numbers for your MiSTer modeline (you need to remove the decimal from 23.876):  
`[video=640x480@59.7]`  
`video_mode=640,32,88,32,480,10,5,10,23876,0,0 ; 640x480@59.7Hz`  
`[video=320x240@59.7]`  
`video_mode=640,32,88,32,480,10,5,10,23876,0,0 ; 320x240@59.7Hz`  
- Put that into your MiSTer.ini file and try it.  You can use Epic Pinball as a test.  You have to start playing for the video mode to be used.
- You should see that the source resolution is 320x240@59.7Hz and the resolution the MiSTer is using is 640x480@59.7Hz.
- The picture is probably not centered. Before proceeding further, adjust the monitor width, height, vertical and horizontal adjustments to their midpoints while displaying this new mode.
- Rather than adjusting the monitor settings to make the screen fit properly, first adjust the modeline to get it centered as much as possible.  After that is finished, fine tune it with the monitor controls.  Use the Left Right Up Down buttons at https://www.epanorama.net/faq/vga2rgb/calc.html to move the picture.  It will move up and down one pixel at a time, but left and right it will move 8 at a time.  You can manually adjust the front porch and back porch numbers in the Horizontal section if you want to move it less than 8 pixels (subtract 5 and add 5 to the numbers for example).  Just see how it adjusts them by 8 and make the same adjustments either positive or negative to where they were before, but by smaller numbers than 8 by typing them in.  Click Calculate and pay attention to the calculated results.  They should not change if you did it right.

- The monitor has the picture in the upper left corner (for example), so try moving it right once, and down 5 times and see how it looks.  In this case the new modeline is:  
`[video=640x480@59.7]`  
`video_mode=640,24,88,40,480,5,5,15,23876,0,0 ; 640x480@59.7Hz`  
`[video=320x240@59.7]`  
`video_mode=640,24,88,40,480,5,5,15,23876,0,0 ; 320x240@59.7Hz`  

- After further testing and adjustments, the final mode is:  
`[video=640x480@59.7]`  
`video_mode=640,4,88,60,480,1,5,19,23876,0,0 ; 640x480@59.7Hz`  
`[video=320x240@59.7]`  
`video_mode=640,4,88,60,480,1,5,19,23876,0,0 ; 320x240@59.7Hz Epic Pinball`  


## For CRT TVs / PVMs (15kHz)

In the case of CRT TV's, you want to have a Horizontal sync frequency between around 15kHz and 16kHz and a vertical sync frequency of around 60Hz.  Again, you should try to match the source's vertical sync frequency to avoid tearing if the source vertical frequency is around the 60Hz range.  If it is not, then you need to use around 60Hz anyway, but getting it exact is no longer important since it can't be exact.  It is a good idea to add these lines to the MiSTer.ini as well to prevent out of range signals:  
`refresh_min=57          ; Makes sure TV can sync the signal, especially in ao486 that can go up to 70 Hz when set to Variable, not 60Hz`  
`refresh_max=62`         ;

The horizontal resolution can go quite high such as 1600, but the vertical resolution should be between 200 and 240 pixels.  A good modeline for the menu is:
`[Menu]`  
`direct_video=0`  
`vga_scaler=1`  
`vsync_adjust=1`  
`vscale_mode=1`  
`video_mode=640,47,56,113,224,16,0,28,13764`  

A good modeline for ao486 with a CRT TV for 320x200 games is:  
`[ao486]`  
`; Set it to "60Hz" in the ao486 core instead of "Variable" unless you are running Second Reality`  
`direct_video=0`  
`vga_scaler=1`  
`vsync_adjust=1`  
`vscale_mode=3`  
`video_mode=640,46,90,140,200,34,0,38,14949 ; Use with vscale_mode=3`  

On CRT's you won't be able to easily, nor should you make monitor sizing adjustments, so you will need to use the modeline if you want to move the image around.  You can also make it wider/narrower and taller/shorter, by first hitting calculate on a mode that is working, then decreasing/increasing the back porch numbers and adjusting the Pixel clock frequency until the View calculated results is back in range again, trying to keep the vertical sync frequency matching the source if possible, and keeping the horizontal sync frequency within ranges the TV can accept.  Changing the back porch number will make it off-center, so you can then adjust it up/down left/right again with those buttons without affecting the calculated results and it should still display on the screen.  Continue making adjustments and testing until you get the sizing and centering where you like it.