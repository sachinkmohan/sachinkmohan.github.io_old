---
layout: post
title:  "Opencv cheat sheet"
date:   2022-03-17 09:00:00 +0200
last_modified_at: 2022-03-17 09:15:00 +0200
permalink: opencv-cheat-sheet
description: Opencv cheat sheet 
published: true
sitemap: true
categories: cheat-sheet
---

**1. Reading files from a folder**
```
import os
import cv2
rootdir = "directory path"
for subdir, dirs, files in os.walk(rootdir):
    for file in files:
        frame = cv2.imread(os.path.join(subdir, file)) 
```
[Ref](https://stackoverflow.com/a/59925514/9063971)

**2. Installing opencv in pip**
```
pip uninstall opencv-python-headless -y 
pip install opencv-python --upgrade
```
[Ref](https://stackoverflow.com/a/70700690/9063971)
