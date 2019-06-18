# Using MiSTer

So, you've got your MiSTer,  now what?
Let's get you setup!



***

You'll need a USB keyboard, and internet for the MiSTer

Make sure both are plugged in, and power on the MiSTer.
The red, orange and green led lights should start pulsing, and you should see the MiSTer menu onscreen after a second or two.



Press F9 to bring up the Linux prompt.

We'll need to download the updater script from Github


(Login with user root, and password 1)

`cd /media/fat/Scripts`

`wget --no-check-certificate https://github.com/MiSTer-devel/Updater_script_MiSTer/blob/master/mister_updater.sh`

`exit`


Once thats downloaded, it should exit back to the prompt.  We can now update the system from within MiSTer.



Tip - Press F12 to bring up the System Menu (if you press F12 again, it will show the core menu).
Use the up and down arrow keys and enter to navigate the menu.

Open up the System Menu.

Navigate to Scripts, then run mister_updater

It will download all the latest cores for you and keep your MiSTer updated.

MiSTer cores are regularly updated - sometimes daily, so run mister_updater regularly!


Ok, you're updated, now what?


***


# Samba Sharing Setup
Lets setup samba sharing.  By default the samba script is disabled, so we need to rename it.
From your MiSTer - 

Press F9 to go to the linux prompt.

(The default user is root, and the default password is 1)

Login as root using the default password

Type or paste the following to enable samba, this will enable samba, and reboot MiSTer

`cd /media/fat/linux`

`mv _samba.sh samba.sh`

`/media/fat/Scripts/samba_on.sh`

`reboot`


If you press F12 again once rebooted, you can see the ip address of your MiSTER in the setup menu.
You can now navigate to your mister via \\IP ADDRESS on windows or smb://IP ADDRESS on Mac.
Check your ip address, and navigate to it.



eg if your ip address is 192.168.0.210

### Windows
`File, Run`

`\\192.168.0.210 `

`to open the share.`


## Mac
`Press APPLE K (cmd K)`

`smb://192.168.0.210`

`Click connect`



***

You'll want to start copying appropriate file backups of your cartridges - i.e. roms to the appropriate locations.


I usually stick my Console or Computer roms in a folder called roms under the root folder, then sort by name under there.

eg

`/roms/Megadrive/...`
`/roms/SNES/...`
`/roms/NES/...`
`etc`


Arcade roms, Computer BIOS and Core system rom's will need to be put elsewhere in a folder called bootrom


`/bootrom/ [ BIOS / Arcade Roms / Core roms go here ] `
***




# Important MiSTer Menu Keys
F12 - brings up the Menu.  Once a Core is loaded, F12 can be used again to load a rom.

ALT F12 - brings up the Core Menu

F1 - changes the background

F11 - bluetooth pairing menu  (for supported BT adaptors)

F9 - Linux prompt (Press F12 to switch back to the MiSTer menu as necessary)

Left Shift + Left Ctrl + Left Alt + Right Alt -  Reboot

Windows + Print Screen - Screenshot

***

# Important Folders or files - what goes where!
Note - If the folders or files don't exist make them!

If you are connecting over SSH or over Linux (F9) on the MiSTer then use the full folder name '/media/fat/...'

**If connecting over SMB, then remove the  `/media/fat/` below as you are already in that folder!**
**eg `/media/fat/menu.jpg` would simply be a file called `menu.jpg` in the root folder**



`/media/fat/menu.jpg or /media/fat/menu.png`

Background menu image for MiSTer (Press F1 to cycle through when in the MiSTer menu).  Needs to be a jpg or a png format file.  MiSTer will resize it for you.


`/media/fat/fonts`

Fonts folder.  Get your fonts [here](https://github.com/MiSTer-devel/Fonts_MiSTer)

Edit /media/fat/MiSTer.ini and edit font=fonts/xxx.pf to your choice of font



`/media/fat/screenshots`

Screenshots taken with Windows Key + PrintScreen will go in here


`/media/fat/bootrom`

Place your rom files in this folder.  Cores will look in this folder first.  Note that Arcade cores need to be built specially for MiSTer and copied in here.  Instructions to build roms are in the core menu per core.

eg Asteroids, you will need to acquire the rom's from, uh, your PCB, and download the files from [here](https://github.com/MiSTer-devel/Arcade-Asteroids_MiSTer/tree/master/releases) - then run the build_rom.sh or bat file to create the MiSTer compatible file -  `a.asteroid.rom` and finally copy that into to `/media/fat/bootrom`.

