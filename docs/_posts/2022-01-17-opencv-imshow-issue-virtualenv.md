---
layout: post
title:  "Opencv imshow error in the virtual environment"
date:   2022-01-17 10:00:00 +0200
last_modified_at: 2022-01-17 11:00:00 +0200
permalink: opencv-imshow-issue-virtualenv
description: how to fix the opencv imshow error in the virtual environment
published: true
sitemap: true
github_comments_issueid: "9"
categories: opencv virtualenv opencv-camera-issue  
---

If you encounter the below error 

```
error: OpenCV(4.1.1) /home/nvidia/host/build_opencv/nv_opencv/modules/highgui/src/window.cpp:352: error: (-215:Assertion failed) size.width>0 && size.height>0 in function 'imshow'
```

or the below

```
OpenCV(4.5.1) C:\Users\appveyor\AppData\Local\Temp\1\pip-req-build-1drr4hl0\opencv\modules\highgui\src\window.cpp:651: error: (-2:Unspecified error) The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Cocoa support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script in function 'cvShowImage'
```

then you can fix it by the below solution

```
pip uninstall opencv-python-headless -y 
pip install opencv-python --upgrade
```

[Reference Link](https://stackoverflow.com/questions/67120450/error-2unspecified-error-the-function-is-not-implemented-rebuild-the-libra/67210407#67210407)
