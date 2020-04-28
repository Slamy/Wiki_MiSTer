You can access the MiSTer through Samba network.
This is native protocol for Windows shares. MiSTer already has FTP and SSH services, but Samba has a special feature - Windows treat Samba shares as a local filesystem. For example, if you want to view or edit the file, then you need to download it fully first in case of FTP/SFTP access. With Samba, only small required portion if file will be loaded. If file has size of 100MB - it makes big difference. Similarly, if you want to use a HEX editor, you don't need to download the whole file. Just open it in HEX editor and only small portion will be loaded where you can quickly edit required bytes and save it back quickly. 
Basically, work with remote files as quick as with local files if you don't need the whole content.
With Samba access you can mount VHD files on your PC without downloading! Using utility [ImDisk](https://sourceforge.net/projects/imdisk-toolkit/) you can mount VHD files as a local disk (mount it as removable store for easier un-mounting).

## Notes:
* By default Samba service is not active. You need to rename **/media/fat/linux/_samba.sh** to **linux/samba.sh**, then edit this file if you need specific user name and password (default is user `root` with pass `1`) and then reboot the MiSTer.
* you can access the MiSTer either by IP address or by name `\\MiSTer` (or `\\mister` - case insensitive).
* The default workgroup for MiSTer's samba share is `MiSTer`
* Make sure you've closed all opened remote files and un-mounted all remote VHDs before restarting the MiSTer or start the cores using the same VHDs in order to prevent the data corruption!
* This can also be accessed from FTP by using **IP address**, login user name `root` with pass `1`.

## Troubleshooting:
If you're using a Windows OS (Vista and above) while trying to access the share and the credentials do not work, there may be a possibility that the LAN Manager authentication level is not being worked out correctly between the Windows OS and the Samba daemon on MiSTer.

The error message may manifest itself as a **The specified network password is not correct** error. A fix is to lower the Samba NTLM authentication level on the MiSTer to NTLM v1.

This is done with the following steps:
1. SSH into your MiSTer instance.
2. Edit the Samba configuration file.
```
nano /etc/samba/smb.conf
```
3. Append under global, where the keyword **yes** signifies ntlmv1-permitted, which allows for NTLMv1 and above for all clients (against MiSTer). By default the value is not set explicitly and is **no**, which equates to ntlmv2-only. Further information is specified in the **ntlm auth (G)** section at [https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html.](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html)
```
[global]
   min protocol = SMB2
   ntlm auth = yes
```
4. Reboot MiSTer or restart the Samba daemon.
```
/etc/init.d/S91smb restart
```
You should see no errors when manually restarting. e.g.
```
/root# /etc/init.d/S91smb restart
Shutting down SMB services: OK
Shutting down NMB services: OK
Starting SMB services: OK
Starting NMB services: OK
```
Alternatively, on the Windows OS, change the Windows registry HKLM\SYSTEM\CurrentControlSet\Control\Lsa\LMCompatibilityLevel to 3. Note that you may/may not have permission depending on your security policy or Administrator rights. This is described by Microsoft at [https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level.](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)
