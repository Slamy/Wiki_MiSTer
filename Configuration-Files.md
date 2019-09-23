## MiSTer.ini

The MiSTer.ini configuration file contains settings for the MiSTer. The file itself can be found here: [MiSTer.ini](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/MiSTer.ini).

![picture](pictures/setup-config-files_mister-ini.png)

Download and copy the `MiSTer.ini` file to the root of your SD-Card. Open it with your favorite editor (e.g. Notepad++) and change the parameters accordingly to the following description.

### key_menu_as_rgui
Makes the MENU key map to RGUI in Minimig (e.g. for Right Amiga)

`key_menu_as_rgui=1` set the MENU key map to RGUI

`key_menu_as_rgui=0` dont set the MENU key map to RGUI

### forced_scandoubler
Run scandoubler on VGA output always (depends on core).

Most modern monitors won't support the 15 KHz horizontal sync output signal through the VGA connector. This option doubles the frequency of horizontal sync signal and brings it in a compatible range for modern monitors. Note that this is not a global option and is only valid for the MiSTer Menu. Each core drives the VGA output itself and requires its own setting. Check the core menu of the corresponding core via HDMI to set the scandoubler option if available / necessary.

`forced_scandoubler=1` activate scandoubler

`forced_scandoubler=0` deactivate scandoubler

### ypbpr
Use YPbPr signal on VGA output.

`ypbpr=1` activate YPbPr

`ypbpr=0` deactivate YPbPr

### composite_sync
Use composite sync as horizontal sync signal on VGA output.

`composite_sync=1` activate composite sync

`composite_sync=0` deactivate composite sync

### vga_scaler
This option connects the VGA to scaler output. (what does this mean? elaborate further)

`vga_scaler=1` connect VGA to scaler output

`vga_scaler=0` disconnect VGA to scaler output


### hdmi_audio_96k
HDMI audio output options

`hdmi_audio_96k=1` 96khz/16bit HDMI audio

`hdmi_audio_96k=0` 48khz/16bit HDMI audio
