---
layout: post
title:  "Flashing AGX Xavier using sdkmanager"
date:   2021-08-25 16:00:00 +0200
last_modified_at: 2022-01-27 12:00:00 +0200
permalink: nvidia-jetson-xavier-agx-flashing-issues-using-sdkmanager
description: How to fix the board not connected jetson error. How to flash the jetson board or how to hard reset the jetson board or how to reset the jetson agx or tx2
published: true
sitemap: true
github_comments_issueid: "1"
categories: [jetson, nvidia, agx-xavier]
---
I used this [simple guide][1] to flash and restore the jetson AGX xavier board.

- If you are getting the below error, then your jetson board is not running on recovery mode.
![Board Not Connected](/assets/flashing-agx-xavier/board_not_connected.jpeg) <br>

- Follow this Wiki to set it to recovery mode first - [Link](https://developer.ridgerun.com/wiki/index.php?title=Xavier/Flashing_the_Board)

- Once it is set to this mode, type `lsusb` and look for **NVIDIA** in the results. Note, you have to plug-in the USB-C cable to the port next to the LED of the
Jetson board as the other one didn't work.

![LSUSB](/assets/flashing-agx-xavier/lsusb.jpeg) <br>

- Now open SDK Manager and see that your board is connected.

![Board Connected](/assets/flashing-agx-xavier/board_connected.jpeg) <br>

### Helpful to identify the recovery button on Jetson AGX Xavier

![Locating recovery button](/assets/flashing-agx-xavier/locating_recovery_button.jpeg) <br>


[1]: https://elinux.org/Jetson/Clone
