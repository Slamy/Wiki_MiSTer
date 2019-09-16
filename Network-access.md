# Network access

MiSTer board can be access through on-board Ethernet port. System has **FTP**, **SSH**, **SFTP** services running.

User name: **root**  Password: **1**

By default, DHCP is used to acquire IP address for the board.
You can find it from your router (easier way), or from console connected to the board using the command **ifconfig**

If you need to set up static IP - please follow Linux manuals (/etc/network/interfaces changes)

**mc** (midnight commander) file manager is available for easier folder navigation.

The root of SD card: **/media/fat**

# Serial Console access
You can connect to the serial console using by attaching the USB mini-B cable to the UART and your computer.  Device name to attach to will depend on your OS.

baud rate: 115200
parity: no
stop bits: 1

More detail about the UART can be found in the DE10-Nano Getting Started Guide and other documentation at http://de10-nano.terasic.com/cd