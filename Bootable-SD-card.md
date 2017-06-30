# How to prepare the SD card.

MiSTer board requires specially formatted SD card in order to boot.
There are 2 options to prepare the SD card.

## Option 1 (Linux system). Preferred.

Preferably Ubuntu 16.04. Make sure you have sfdisk v2.26 or newer installed.

Steps to prepare the SD card:
1. Download [SD Installer](https://github.com/MiSTer-devel/SD-installer_MiSTer) repository.
2. Insert SD card into PC (directly or through card reader) and find the device name of the card. Usually type lsblk in command line and find your card in the list. For example it's listed as "sdc"
3. in command line navigate to the directory where you've downloaded SD installer and type: **sudo ./create_sd.sh /dev/'dev'**, so in our case 'dev' is sdc, so command will be **sudo ./create_sd.sh /dev/sdc**

**ATTENTION: installer will remove all information from SD card, so make sure you type the correct SD card's device name!**

Installer will create required partitions and put all Linux related files. Approximately 500MB of card space will be occupied by Linux. The rest of the card will be assigned to FAT partition and left unformatted. 

4. Format the FAT partition manually. Windows will see only FAT partition, so you can format it using standard windows format utility. FAT partition can be formatted either with FAT32 or exFAT. I recommend to format with exFAT - it supports partitions >32GB and files >4GB. Choose cluster size 32KB or 64KB while formatting. Smaller cluster size will slowdown the booting and file loading.

5. Place [MiSTer](https://github.com/MiSTer-devel/Main_MiSTer/tree/master/releases) and [Menu.rbf](https://github.com/MiSTer-devel/Menu_MiSTer/tree/master/releases) binaries on FAT partition. Remove date-codes from names.

## Option 2 (Windows system)

1. Download [SD image](https://mega.nz/#F!tIQAHAQI!9D58SzVMLBE6VIyq4cZPZA)
2. Download [HDD Raw Copy Tool](http://hddguru.com/software/HDD-Raw-Copy-Tool/). Portable version is fine.
3. Insert SD card (2GB or bigger) into PC (directly or through card reader) and restore the image.

You will get an SD card where only 2GB will be used with 1.3GB of FAT partition. Even if SD card is 64GB, only 2GB will be available. You can try to use some disk management/copy tool to expand the FAT partition, but most likely tool will mess the partition order and you won't see a FAT partition in Windows anymore.

So, there are additional steps to make a SD card and make the whole card space available. In this case you need 2 SD cards. The first SD card will be temporary card with small size. Prepare it as in described in steps 1-3. For steps 4 and up use a second SD card which you intend to use for MiSTer.

4. Plug temporary SD card into DE10-nano board and boot.
5. Using any console application, connect to DE10-nano board using its USB-serial port (next to micro-USB port).
6. Login to DE10-nano using name: **root** and password **1**
7. Using SD card reader plug your main SD card into DE10-nano's USB (micro-USB. Use USB hub if single port is not enough).
8. Wait for several seconds, so system will recognize it.
9. type **makesd** and it will format your SD card on USB port. 
10. Follow steps 4 and 5 of **Option 1**.



***

## Notes:

* Time after time Linux part will be updated, so you need to update the SD card. Due to FAT partition hasn't touched by installer, everything on FAT partition will be left as-is (if you didn't alter the FAT partition size by other tools). So it's safe to update the Linux part on already prepared SD card.
* MiSter allows to use USB storage for cores and their data, but boots only from SD card. Thus you can use the minimal SD card image from Option 2 just to boot, and use USB storage for everything else.
* USB storage needs significantly longer time to be detected. This time required whenever you power on the board, press reset button or hard reset keyboard configuration. Once USB detected, you can reload the cores without waiting.
* Don't forget to update MiSter and menu.rbf files if you want to be up to date. SD image may not have lates MiSTer and/or menu.rbf, so update them manually after restore the image.
* As probably you've noticed, bootable SD card contains installer as well. So, you can make/repair other SD cards using DE10-nano board from console app. Just use steps from 5 of **Option 2**.

## Troubleshooting:
1. How to determine SD-card device name in Linux?

  Run _lsblk_ command. It will show all block devices in a system (All SSDs/HDDs/SD card devices).

![SD card example](http://image.ibb.co/cjdv7k/Screen_Shot_2017_06_30_at_11_52_16_AM.png)

/dev/sdb - SD card disk itself, having a single partition /dev/sdb1 on it.

You need to execute "sudo ./create_sd.sh /dev/sdb" command to execute card installation actions.

Example output:
> $ sudo ./create_sd.sh /dev/sdb

> Do you wish to partition this SD card? y

> Unmounting some partitions (errors are ok here)...
> umount: /dev/sdb: not mounted
> umount: /dev/sdb1: not mounted
> umount: /dev/sdb2: mountpoint not found
> umount: /dev/sdb3: mountpoint not found

> Erasing of first 64MB of card...
> 64+0 records in
> 64+0 records out
> 67108864 bytes (67 MB, 64 MiB) copied, 9.37422 s, 7.2 MB/s
> Partitioning...
> Checking that no-one is using this disk right now ... OK

> Disk /dev/sdb: 29 GiB, 31104958464 bytes, 60751872 sectors
> Units: sectors of 1 * 512 = 512 bytes
> Sector size (logical/physical): 512 bytes / 512 bytes
> I/O size (minimum/optimal): 512 bytes / 512 bytes

> >>> Created a new DOS disklabel with disk identifier 0x3eb96104.
> Created a new partition 1 of type 'W95 FAT32' and of size 28.5 GiB.
> /dev/sdb2: Created a new partition 2 of type 'Linux' and of size 500 MiB.
> /dev/sdb3: Created a new partition 3 of type 'Unknown' and of size 1023.5 KiB.
> /dev/sdb4: 
> New situation:

> Device     Boot   Start      End  Sectors    Size Id Type
> /dev/sdb1       1028096 60751871 59723776   28.5G  b W95 FAT32
> /dev/sdb2          4096  1028095  1024000    500M 83 Linux
> /dev/sdb3          2048     4094     2047 1023.5K a2 unknown

> Partition table entries are not in disk order.

> The partition table has been altered.
> Calling ioctl() to re-read partition table.
> Syncing disks.

> Unmounting some partitions (errors are ok here)...
> umount: /media/rootfs: mountpoint not found
> Formatting Linux partition...
> mke2fs 1.42.13 (17-May-2015)
> Creating filesystem with 512000 1k blocks and 128016 inodes
> Filesystem UUID: 86bf2979-9185-4972-bdcf-757cf1e98e8e
> Superblock backups stored on blocks: 
> 	8193, 24577, 40961, 57345, 73729, 204801, 221185, 401409

> Allocating group tables: done                            
> Writing inode tables: done                            
> Creating journal (8192 blocks): done
> Writing superblocks and filesystem accounting information: done 


> Copying U-Boot loader...
> 1012+1 records in
> 1012+1 records out
> 518215 bytes (518 kB, 506 KiB) copied, 0.0509648 s, 10.2 MB/s
> Mounting Linux partition...
> Copying main rootfs files...
> Copying kernel modules rootfs files...
> Copying devices firmwares...
> Copying additional modifications...
> Copying kernel...
> Copying this installer...
> Fixing permissions...
> Unmounting Linux partition...
> Done!
