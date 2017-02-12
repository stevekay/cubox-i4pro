# Installing Debian 7 wheezy on cubox-i4pro.

Notes based on following https://gist.github.com/richardjortega/b7c5435f2cd1f8f75298 and https://people.debian.org/~gwolf/

## On a Linux VM, download Debian image

    [root@localhost ~]# df -h .
    Filesystem           Size  Used Avail Use% Mounted on
    /dev/mapper/cl-root  8.0G  7.5G  524M  94% /
    [root@localhost ~]# wget https://people.debian.org/~gwolf/cubox.img.xz
    --2017-02-11 20:49:18--  https://people.debian.org/~gwolf/cubox.img.xz
    Resolving people.debian.org (people.debian.org)... 5.153.231.30, 2001:41c8:1000:21::21:30
    Connecting to people.debian.org (people.debian.org)|5.153.231.30|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 105133096 (100M) [application/x-xz]
    Saving to: ‘cubox.img.xz’
    
    100%[======================================>] 105,133,096 5.76MB/s   in 17s
    
    2017-02-11 20:49:35 (5.94 MB/s) - ‘cubox.img.xz’ saved [105133096/105133096]
    
    [root@localhost ~]# xz -d cubox.img.xz
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
    [root@localhost ~]# time dd if=cubox.img of=/dev/sdb
    1445890+0 records in
    1445890+0 records out
    740295680 bytes (740 MB) copied, 1398.93 s, 529 kB/s
    
    real    23m18.941s
    user    0m0.348s
    sys     0m11.771s
    [root@localhost ~]#

## Insert SD card into cubox, boot up, login

On usb keyboard, logon as root, password cubox-i.

## Add network details

    root@cubox-i:~# echo 'auto eth0' >>/etc/network/interfaces
    root@cubox-i:~# echo 'iface eth0 inet dhcp' >>/etc/network/interfaces
    root@cubox-i:~# ifdown eth0
    root@cubox-i:~# ifup eth0
    Internet Systems Consortium DHCP Client 4.2.2
    Copyright 2004-2011 Internet Systems Consortium.
    All rights reserved.
    For info, please visit https://www.isc.org/software/dhcp/
    
    Listening on LPF/eth0/d0:63:b4:00:3e:40
    Sending on   LPF/eth0/d0:63:b4:00:3e:40
    Sending on   Socket/fallback
    DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 4
    DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 10
    DHCPREQUEST on eth0 to 255.255.255.255 port 67
    DHCPOFFER from 192.168.0.1
    DHCPACK from 192.168.0.1
    bound to 192.168.0.17 -- renewal in 40960 seconds.
    root@cubox-i:~#

## Install ssh
  
    root@cubox-i:~# apt-get install ssh

## Log onto cubox via ssh instead of using USB keyboard

    [root@localhost ~]# ssh 192.168.0.17
