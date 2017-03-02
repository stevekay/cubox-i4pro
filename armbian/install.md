# Installing armbian Jessie on cubox-i4pro.

armbian cubox-i page is https://www.armbian.com/cubox-i/

## On a Linux VM, download armbian image

    [root@localhost ~]# wget https://dl.armbian.com/cubox-i/Debian_jessie_next.7z
    [root@localhost ~]# yum install -y p7zip
    [root@localhost ~]# 7za e Debian_jessie_next.7z
    [root@localhost ~]# ls -l
    total 1489872
    -rw-r--r--. 1 root  root  1317011456 Feb  5 22:47 Armbian_5.25_Cubox-i_Debian_jessie_next_4.9.7.img
    -rw-r--r--. 1 root  root         819 Feb  5 22:48 Armbian_5.25_Cubox-i_Debian_jessie_next_4.9.7.img.asc
    -rw-r--r--. 1 root  root       18574 Feb  5 22:47 armbian.txt
    -rw-r--r--. 1 root  root         819 Feb  5 22:48 armbian.txt.asc
    -rw-rw-r--. 1 root  root   208581339 Feb  6 00:48 Debian_jessie_next.7z
    -rw-r--r--. 1 root  root         116 Feb  5 22:47 sha256sum.sha
    [root@localhost ~]# 

## Insert SD card (/dev/sdb), write image to it

    [root@localhost ~]# fdisk -l /dev/sdb
    
    Disk /dev/sdb: 7892 MB, 7892631552 bytes, 15415296 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0xf56c4ddc
    
    Device Boot      Start         End      Blocks   Id  System
    /dev/sdb1   *        2048       34815       16384    e  W95 FAT16 (LBA)
    /dev/sdb2           34816    15415295     7690240   83  Linux
    [root@localhost ~]# dd if=Armbian*img of=/dev/sdb bs=1M
    [root@localhost ~]#

## Insert SD card into cubox, boot up, login

On usb keyboard, logon as root, password 1234.
