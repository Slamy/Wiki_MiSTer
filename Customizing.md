The MiSTer menu can be customized in a number of ways.

eg You can add a cool font, or change the background image for the main menu.


# To change the default font

Create a /media/fat/fonts folder on your SD card.


Next download the fonts from here - [MiSTer Fonts](https://github.com/MiSTer-devel/Fonts_MiSTer)

Copy the pf files downloaded from that url to the /media/fat/fonts folder


Next edit /media/fat/MiSTer.ini


Find the 

font= line, and edit to use a new font.  Be careful not to add a / before the font folder!


eg

If you want to use the C64 font - change the font line to 

font=fonts/Computer_C64.pf



# To add a background image


Find a suitable png or jpg file that you like

Copy your desired image to /media/fat/menu.jpg or /media/fat/menu.png (as appropriate)

reboot


Press F1 once rebooted into MiSTer to select your background.


