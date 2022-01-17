---
layout: post
title:  "Resizing the camera frame to a specific dimension required for your inference"
date:   2022-01-14 16:00:00 +0200
last_modified_at: 2022-01-14 15:00:00 +0200
permalink: resizing-the-camera-frame
description: How to resize the original camera dimensions for inference in live object detection
published: true
sitemap: true
github_comments_issueid: "6"
categories: [opencv, tensorflow, pytorch]
---

In the below example I have resized the frames from the camera to 320 * 480(weight * height)

```
import cv2
cap = cv2.VideoCapture(0)

while cap.isOpened():
    ret, frame = cap.read()
    image_resized2 = cv2.resize(frame, (480,320))
```
