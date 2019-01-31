You can access the MiSTer through Samba network.
This is native protocol for Windows shares. MiSTer already has FTP and SSH services, but Samba has a special feature - Windows treat Samba shares as a local filesystem. For example, if you want to view or edit the file, then you need to download it fully first in case of FTP/SFTP access. With Samba, only small required portion if file will be loaded. If file has size of 100MB - it makes big difference. Similarly, if you want to use a HEX editor, you don't need to download the whole file. Just open it in HEX editor and only small portion will be loaded where you can quickly edit required bytes and save it back quickly. 
Basically, work with remote files as quick as with local files if you don't need the whole content.
With Samba access you can mount VHD files on your PC without downloading! Using utility [ImDisk](https://sourceforge.net/projects/imdisk-toolkit/) you can mount VHD files as a local disk (mount it as removable store for easier un-mounting).

## Notes:
* By default Samba service is not active. You need to rename **/media/fat/linux/_samba.sh** to **linux/samba.sh**, then edit this file if you need specific user name and password (default is user **root** with pass **1**) and then reboot the MiSTer.
* you can access the MiSTer either by IP address or by name **\\\\MiSTer** (or **\\\\mister** - case insensitive).
* Make sure you've closed all opened remote files and un-mounted all remote VHDs before restarting the MiSTer or start the cores using the same VHDs in order to prevent the data corruption!
* This can also be accessed from FTP by using **IP address**, login user name **root** with pass **1**.

## Troubleshooting:
* If you're using a Windows OS (Vista and above) to access the share and the credentials do not work (even though it should) and receive the **The specified network password is not correct** error, chances are that the Windows machine is not negotiating with NTLMv2 against the samba daemon on MiSTer. According to [https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html), the default is for ntlm auth is set at ntlmv2-only (alias no), which is **Do not allow NTLMv1 to be used, but permit NTLMv2.**

You can verify this by executing the following on the command line:

```
reg query HKLM\SYSTEM\CurrentControlSet\Control\Lsa /v LMCompatibilityLevel
```
If the result is 0x0, 0x1, or 0x2, you need to add a setting to the /etc/samba/smbd.conf file (preferred), or the Windows OS client.

**TL;DR**

Choose one:
1. Add under global, in /etc/samba/smb.conf on your MiSTer. When editing, please make sure that you're using Unix LF EOL characters. Windows notepad will not do it unless you modify registry settings described in: [https://blogs.msdn.microsoft.com/commandline/2018/05/08/extended-eol-in-notepad/](https://blogs.msdn.microsoft.com/commandline/2018/05/08/extended-eol-in-notepad/)
```
[global]
ntlm auth = ntlmv1-permitted
```
2. Change HKLM\SYSTEM\CurrentControlSet\Control\Lsa\LMCompatibilityLevel to 3. Note that you may/may not have permission depending on the security policy.
