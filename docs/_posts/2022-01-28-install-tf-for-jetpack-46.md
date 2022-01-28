---
layout: post
title:  "Install tensorflow for jetson jetpack 46 or 4.6"
date:   2022-01-28 13:00:00 +0200
last_modified_at: 2022-01-28 13:15:00 +0200
permalink: tensorflow-jetson
description: How to install tensorflow for jetson agx xavier jetpack 4.6 or jpv46
published: true
sitemap: true
categories: [tensorflow-installation-jetson, agx-xavier]  
---

The standard packages are not working as described in this [link](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform-release-notes/tf-jetson-rel.html#tf-jetson-rel)

You can use the below to install for Jetpack 4.6.

`sudo pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v461 tensorflow==1.15.5`

Found this new directory under the given link, which was uploaded on 26th Jan 2022. They have 2 versions, one is for `1.15.5` and for the stable version `2.7.0`

https://developer.download.nvidia.com/compute/redist/jp/v461/tensorflow/
