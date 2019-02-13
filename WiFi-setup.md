Starting from Release 20180115 MiSTer supports some WiFi USB modules.

### Enable WiFi connection
* locate the file **linux/_wpa_supplicant.conf**
* open in text editor **supporting Linux/Unix** line endings (for example Notepad++)
* replace **put_your_SSID_here** with your actual WiFi network name and **put_your_password_here** with your WiFi password.
* rename **_wpa_supplicant.conf** to **wpa_supplicant.conf**
* reboot the MiSTer

In Menu core you will see WiFi icon when WiFi is connected.

## WiFi USB dongles Confirmed to work
* ASUS USB AC53 nano rev A1.
* D-Link DWA-171 HWVer: A1.
* Edimax EW-7811UN
* TP-LINK TL-WN823N V2 (needs copy rtl8192eu_nic.bin to /lib/firmware/rtlwifi)


Some WiFi firmwares can be found here: https://github.com/wkennington/linux-firmware

## Compiling and installing custom WiFi drivers

Instructions for rtl8188fu based adapters (like the Zapo RTL8188 USB stick) can be read here: 
[MiSTer custom WiFi driver compilation](https://gist.github.com/nistvan86/5c36ad73b8943321dd1bec30da567e6c)
Steps can be adapted for other WiFi adapters.