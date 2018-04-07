Recent release added support for serial (UART) connection from FPGA to Linux. Linux OS runs PPP or Console daemon on this connection allowing to access the internet or Linux shell from FPGA cores.

## Cores supporting serial connection
* Minimig. Tested on Roadshow TCP/IP and AmiTCP. AmiTCP provides more complete solution with ftpd daemon. There are many other 3rd party addons are based on AmiTCP, so it's advised to use this package. Roadshow works ok locally, although i couldn't make DNS work. Probably it needs more settings, but their 20min demo doesn't allow to test and setup it fully. Term v4.7 has been used to test console connection.
* ao486. Currently only console connection has been tested using Dos Navigator's integrated Terminal and Kermit 3.15. PPP should work under Win95.

OSD provides an option to switch between PPP and Console on these cores.
Both console and PPP are using baud rate 115200 8N1 mode with hardware RTS/CTS flow control for stability.

## Console connection
Using this connection with supported terminal application on FPGA core, you can access the Linux shell and do some file managements or Linux settings if required.
No special settings are required of Linux. 

## PPP connection
Using this connection core may have internet connection. More important, the core may run ftp daemon and provide access to its filesystem, so you can use FTP client on PC to move the files to/from the emulated system.

PPP daemon uses /media/fat/linux/ppp_options (linux\ppp_options of PC) file and it requires adjustment according to your network setting. Basically only last line of file with IP addresses may require change. Please read a small instruction in the same file at the end.


NOTE: I'm looking Amiga and MSDOS terminal supporting color and control codes of linux, so it will be possible to use Midnight Commander in terminal connection. If you know such terminal application, then let me know.