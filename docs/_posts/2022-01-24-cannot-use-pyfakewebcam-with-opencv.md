---
layout: post
title:  "Unable to use pyfakeWebcam with opencv"
date:   2022-01-24 13:00:00 +0200
last_modified_at: 2022-01-24 13:00:00 +0200
permalink: unable-to-use-pyfakewebcam-opencv
description: How to use pyfakewebcam with opencv
published: true
sitemap: true
categories: [opencv]  
---

If you are getting this error while using pyfakewebcam with opencv from this well explained [blog](https://memotut.com/en/696ffb48e154b65fb4d1/)

`TypeError: Expected Ptr<cv::UMat> for argument '%s'`


```
import cv2
import pyfakewebcam

import numpy as np

gray = pyfakewebcam.FakeWebcam('/dev/video0', 640, 480)

while(True):
    # Capture frame-by-frame

    print('Type of gray ->', type(gray))
    gray = cv2.resize(gray, (500, 300))
    
    
    cv2.imshow("Pyfakewebcam", gray)

    key = cv2.waitKey(1)
    if key == 27:
        break

gray.release()
cv2.destroyAllWindows()
```

![error_pyfakewebcam](https://user-images.githubusercontent.com/26414662/150806492-eddef48d-6c31-4e63-849a-c4522e1fc07d.png)


If you look closely, I have printed the type of the image that we are getting from `pyfakewebcam`. It is not a `np.ndarray` as we get from opencv.
Hence we cannot use this pyfakewebcam for opencv operations.
