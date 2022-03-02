---
layout: post
title:  "Jetson Inference hacks"
date:   2022-01-18 16:00:00 +0200
last_modified_at: 2022-01-18 15:00:00 +0200
permalink: jetson-inference-hacks
description: Collecting all the hacks here
published: true
sitemap: true
github_comments_issueid: "10"
categories: [jetson]
---

- Releasing the memory occupied by tensorflow

```
from numba import cuda 
device = cuda.get_current_device()
device.reset()
```
