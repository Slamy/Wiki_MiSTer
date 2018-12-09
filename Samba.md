You can access the MiSTer through Samba network.
This is native protocol for Windows shares. MiSTer already has FTP and SSH services, but Samba has a special feature - Windows treat Samba shares as a local filesystem. For example, if you want to view or edit the file, then you need to download it fully first in case of FTP/SFTP access. With Samba, only small required portion if file will be loaded. If file has size of 100MB - it makes big difference. Similarly, if you want to use a HEX editor, you don't need to download the whole file. Just open it in HEX editor and only small portion will be loaded where you can quickly edit required bytes and save it back quickly. 
Basically, work with remote files as quick as with local files if you don't need the whole content.
With Samba access you can mount VHD files on your PC without downloading! Using utility [ImDisk](https://sourceforge.net/projects/imdisk-toolkit/) you can mount VHD files as a local disk (mount it as removable store for easier un-mounting).

## Notes:
* By default Samba service is not active. You need to rename **linux/_samba.sh** to **linux/samba.sh**, then edit this file if you need specific user name and password (default is user **root** with pass **1**) and then reboot the MiSTer.
* you can access the MiSTer either by IP address or by name **\\\\MiSTer** (or **\\\\mister** - case insensitive).
* Make sure you've closed all opened remote files and un-mounted all remote VHDs before restarting the MiSTer or start the cores using the same VHDs in order to prevent the data corruption!
*/media/fat/linux is where _samba.sh is located.  This can also be accessed from FTP IP address login name:root pw:1