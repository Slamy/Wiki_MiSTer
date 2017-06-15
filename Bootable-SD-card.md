MiSTer board requires specially formatted SD card in order to boot.
There are 2 options to prepare the SD card.

## Option 1 (Linux system). Preferred.

Preferably Ubuntu 16.04. Make sure you have sfdisk v2.26 or newer installed.

Steps to prepare the SD card:
1. Download [SD Installer](https://github.com/MiSTer-devel/SD-installer_MiSTer) repository.
2. Insert SD card into PC (directly or through card reader) and find the device name of the card. Usually type lsblk in command line and find your card in the list. For example it's listed as "sdc"
3. in command line navigate to the directory where you've downloaded SD installer and type: **sudo ./create_sd.sh /dev/<dev>**, so in our case <dev> is sdc, so command will be **sudo ./create_sd.sh /dev/sdc**

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
10. Follow step 4 in **Option 1**.


