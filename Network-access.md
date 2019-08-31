# Network access

MiSTer board can be access through on-board Ethernet port. System has **FTP**, **SSH**, **SFTP** services running.

User name: **root**  Password: **1**

By default, DHCP is used to acquire IP address for the board.
You can find it from your router (easier way), or from console connected to the board using the command **ifconfig**

If you need to set up static IP - please follow Linux manuals (/etc/network/interfaces changes)

**mc** (midnight commander) file manager is available for easier folder navigation.

The root of SD card: **/media/fat**
