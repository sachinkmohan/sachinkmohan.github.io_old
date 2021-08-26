---
layout: post
title:  "Flashing AGX Xavier"
date:   2021-08-25 16:00:00 +0200
last_modified_at: 2021-08-25 16:00:00 +0200
permalink: nvidia-jetson-xavier-agx-flashing-issues
description: How to fix the board not connected jetson error. How to flash the jetson board or how to hard reset the jetson board or how to reset the jetson agx or tx2
published: true
sitemap: true
categories: jetson nvidia agx-xavier
---

- If you are getting the below error, then your jetson board is not running on recovery mode.
![Board Not Connected](/assets/flashing-agx-xavier/board_not_connected.jpeg) <br>

- Follow this Wiki to set it to recovery mode first - [Link](https://developer.ridgerun.com/wiki/index.php?title=Xavier/Flashing_the_Board)

- Once it is set to this mode, type `lsusb` and look for **NVIDIA** in the results

![LSUSB](/assets/flashing-agx-xavier/lsusb.jpeg) <br>

- Now open SDK Manager and see that your board is connected.

![Board Connected](/assets/flashing-agx-xavier/board_connected.jpeg) <br>

### Helpful to identify the recovery button on Jetson AGX Xavier

![Locating recovery button](/assets/flashing-agx-xavier/locating_recovery_button.jpeg) <br>



