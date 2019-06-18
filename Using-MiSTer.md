# Using MiSTer

So, you've got your MiSTer,  now what?
Let's get you setup!

You'll need a USB keyboard, and internet for the MiSTer

Make sure both are plugged in, and power on the MiSTer.
The red, orange and green led lights should start pulsing, and you should see the MiSTer menu onscreen after a second or two.

Press F12 to bring up the System Menu (if you press F12 again, it will show the core menu).
Use the up and down arrow keys and enter to navigate the menu.

Suggested first things - open up the System Menu.

Navigate to Scripts

Find and run Update

Assuming you have some internet, it will download another script called mister_updater for you

Press F12 again, go to Scripts, then run mister_updater

It will download all the latest cores for you and keep your MiSTer updated.

MiSTer cores are regularly updated - sometimes daily, so run mister_updater regularly!


Ok, you're updated, now what?


# Samba Sharing Setup
Lets setup samba sharing.  By default the samba script is disabled, so we need to rename it.

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
eg if your ip address is 192.168.0.210

### Windows
`File, Run`
`\\192.168.0.210 `
`to open the share.`

## Mac
`APPLE K`
`smb://192.168.0.210`
`and click connect`




# Important MiSTer Menu Keys
F12 - brings up the Menu

ALT F12 - brings up the Core Menu

F1 - changes the background

F11 - bluetooth pairing menu  (for supported BT adaptors)

F9 - Linux prompt

Left Shift + Left Ctrl + Left Alt + Right Alt -  Reboot

