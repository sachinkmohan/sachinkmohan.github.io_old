---
layout: post
title:  "Installing Tensorflow 1.15 from the source on Jetson AGX Xavier"
date:   2021-11-27 18:00:00 +0200
last_modified_at: 2021-11-27 17:02:00 +0200
permalink: installing-tf-115-on-jetson-agx-xavier
description: Installation instructions
published: true
sitemap: true
github_comments_issueid: "5"
categories: [agx-xavier]
---

I followed the wonderful [blog of JK Jung](https://jkjung-avt.github.io/build-tensorflow-1.12.2/) and everything installed fine except step 5. In my case I had to install TF 1.15 and I installed the proper version of Bazel and protobuf as mentioned in his github page. 

The installation broke several times, unless I fixed the package versions to the below for TF 1.15. Every failed installation costed me around 3-3.5 hours on an averaged.

```
sudo pip3 install -U 'numpy<1.19.0'
sudo pip3 install -U h5py==2.10.0
sudo pip3 install pandas
sudo pip3 install future
sudo pip3 install -U keras_applications==1.0.8 --no-deps
sudo pip3 install -U keras_preprocessing==1.1.2 --no-deps
```

Also I felt the patch in the `install_tf.sh` didn't help my installation either and kept failing. 

Finally I installed these packages manually step by step and followed this standard [TF installation guide](https://www.tensorflow.org/install/source).

> Every time the build fails, it doesn't give proper reasons and was annoying. 

The output of `bazel build --verbose_failures` didn't give much information as well. 

> Finally after 5.5 hours and 29363 actions/steps later, the build was completed successfully. That moment of joy is unexplainable :D 


Good Luck! 

Other links which helped me are: 

[1](https://forums.developer.nvidia.com/t/building-tensorflow-1-13-on-jetson-xavier/75966)
[2](https://www.bojankomazec.com/2019/12/how-to-build-tensorflow-20-on-jetson.html)
