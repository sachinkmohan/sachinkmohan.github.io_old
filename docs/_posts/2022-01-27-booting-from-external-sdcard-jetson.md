
---
layout: post
title:  ""
date:   2022-01-27 16:00:00 +0200
last_modified_at: 2022-01-27 17:00:00 +0200
permalink: booting-from-external-sdcard-jetson
description: How to boot jetson or jetson agx xavier using external SD card.
published: true
sitemap: true
categories: [jetson, jetson-agx]  
---

8b883b8b-a353-4526-9532-67b1f96cf62d

Conclusion: Doesn't matter, if fstab is created in /lib/init folder of the external SD card. Doesn't matter that either on /etc/fstab on the EMMC.
What only matters is what you edit in the file extlinux.conf in the internal EMMC. `vim /boot/extlinux/extlinux.conf`, just change `mmcblk0p1` to `mmcblk1p1`


`mount | head -n 1` -> Tell which partition your OS is booted from 

So I changed the original EMMC `extlinux.conf(/boot/extlinux/extlinux.conf)` 
My original `extlinux.conf` looks like below. I changed the `mmbclk0p1` to `mmbclk1p1` and then things started working. My SD card booted after that.
```
**************************************************************************************************************************************
TIMEOUT 30
DEFAULT primary

MENU TITLE L4T boot options

LABEL primary
      MENU LABEL primary kernel
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} quiet root=/dev/mmcblk1p1 rw rootwait rootfstype=ext4 console=ttyTCU0,115200n8 console=tty0 fbcon=map:0 net.ifnames=0 rootfstype=ext4

# When testing a custom kernel, it is recommended that you create a backup of
# the original kernel and add a new entry to this file so that the device can
# fallback to the original kernel. To do this:
#
# 1, Make a backup of the original kernel
#      sudo cp /boot/Image /boot/Image.backup
#
# 2, Copy your custom kernel into /boot/Image
#
# 3, Uncomment below menu setting lines for the original kernel
#
# 4, Reboot

LABEL backup
      MENU LABEL backup kernel
      LINUX /boot/Image.backup
      INITRD /boot/initrd
      APPEND ${cbootargs}


**************************************************************************************************************************************
```

This worked, I have also made changes in `/etc/fstab` and `/media/ubuntu/UUID/lib/init/fstab` 
I am not sure, if these things have made really any impact. Need to check this.

I also edited the `/media/ubuntu/UUID/boot/extlinux/extlinux.conf` and those settings didn't work as described in jetson hacks. Probably it was written in 2017
for old jetpack versions and different versions R32. 


In summary, the problem was resolved when I edited the `/boot/extlinux/extlinux.conf` on the jetson board and not the one on the SD card as the jetson company decided to not 
scan SD card inserted and to read from the internal EMMC first about the boot priorities.


Below is the SD card extlinux.conf and this didn't work at all.

```
--------------------------------------------------------------------------------------------------------------------------------------
TIMEOUT 30
DEFAULT sdcard

MENU TITLE L4T boot options

LABEL sdcard
      MENU LABEL SD Card
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} quiet root=/dev/mmcblk1p1 rw rootwait rootfstype=ext4 console=ttyTCU0,115200n8 console=tty0 fbcon=map:0 net.ifnames=0 rootfstype=ext4 


LABEL internalemmc
      MENU LABEL Internal EMMC
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} quiet root=/dev/mmcblk0p1 rw rootwait rootfstype=ext4 console=ttyTCU0,115200n8 console=tty0 fbcon=map:0 net.ifnames=0 rootfstype=ext4 

# When testing a custom kernel, it is recommended that you create a backup of
# the original kernel and add a new entry to this file so that the device can
# fallback to the original kernel. To do this:
#
# 1, Make a backup of the original kernel
#      sudo cp /boot/Image /boot/Image.backup
#
# 2, Copy your custom kernel into /boot/Image
#
# 3, Uncomment below menu setting lines for the original kernel
#
# 4, Reboot

# LABEL backup
#    MENU LABEL backup kernel
#    LINUX /boot/Image.backup
#    INITRD /boot/initrd
#    APPEND ${cbootargs}

--------------------------------------------------------------------------------------------------------------------------------------
```
