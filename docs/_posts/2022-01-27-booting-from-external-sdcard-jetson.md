---
layout: post
title:  "Booting Jetson Xavier AGX from the SD Card"
date:   2022-01-27 16:00:00 +0200
last_modified_at: 2022-01-27 17:00:00 +0200
permalink: booting-from-external-sdcard-jetson
description: How to boot jetson or jetson agx xavier using external SD card.
published: true
sitemap: true
categories: [jetson-agx]  
---

First of all, I would like to thank Jetson Hacks for creating a wonderful [tutorial](https://www.jetsonhacks.com/2017/01/26/run-jetson-tx1-sd-card/)

I just followed everything as described in his blog until the part where I had to edit the `extlinux.conf` file. 

So below instructions is just an add-on to his blog on that part alone for Jetson AGX Xavier.

`mount | head -n 1` -> Tells which partition your OS is booted from -> A command which is very hand in the end to check where the OS is booting from. So make 
sure you enter this before and after making the changes on the Jetson board.

So I changed the original EMMC(i.e on the Jetson board itself without the SD card) `extlinux.conf(/boot/extlinux/extlinux.conf)` 
My original `extlinux.conf` looks like below after the change. Make sure you take a backup as suggested by jetsonhacks in his blog and video. I changed the `mmbclk0p1` to `mmbclk1p1` and then things started working. My jetson board booted after that from the SD card. Yes, don't be surprised, that's the only change I did. But there is one problem. If you remove the SD, the device will not boot again. So if you wish to boot it again from the internal EMMC, make sure you reset it back to the original state. Yeah, it's a pretty dirty hack. But it works!!

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

There are some changes in `/etc/fstab` and `/media/ubuntu/UUID/lib/init/fstab` that I read on the various forums.
You can ignore this. I didn't do any changes. 

I also edited the `/media/ubuntu/UUID/boot/extlinux/extlinux.conf` and those settings didn't work as described in jetson hacks. Probably it was written in 2017
for old jetpack versions and different versions R32. 

In summary, the problem was resolved when I edited the `/boot/extlinux/extlinux.conf` on the jetson board and not the one on the SD card. Probably Nvidia or Jetson team decided not to scan the SD card inserted, as it is supposed to be in the boot priority.

**Note** - This gives us an advantage that next time if you mess up the SD card, just format the SD card and then copy the image from the eMMC to the SD card again as explained in the jethacks blog. Make sure that you change the settings to `root=/dev/mmcblk0p1` in the eMMC.


_Ignore the below_ \
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\
Doesn't matter, if fstab is created in `/lib/init` folder of the external SD card. Doesn't matter that either on `/etc/fstab` on the EMMC.
What only matters is what you edit in the file extlinux.conf in the internal EMMC. `vim /boot/extlinux/extlinux.conf`, just change `mmcblk0p1` to `mmcblk1p1` \
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
