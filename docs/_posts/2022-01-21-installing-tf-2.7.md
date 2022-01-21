---
layout: post
title:  "Installing tensorflow 2.7 in pip environment"
date:   2022-01-21 16:00:00 +0200
last_modified_at: 2022-01-21 15:00:00 +0200
permalink: installing-tensorflow-2.7
description: how to install tensorflow 2.7 in the pip environment
published: true
sitemap: true
github_comments_issueid: "11"
categories: [tensorflow2-installation, tensorflow]
---

Though I am a huge fan of conda, and wanted to install tensorflow 2.7, but unfortunately i couldn't find a conda version `conda search -c conda-forge tensorflow-gpu`,

Then I executed `$ pip install tensorflow-gpu==2.7.0`

which gave me the following error

```
ERROR: Could not find a version that satisfies the requirement tensorflow-gpu==2.7.0 (from versions: 0.12.1, 1.0.0, 1.0.1, 1.1.0, 1.2.0, 1.2.1, 1.3.0, 1.4.0, 1.4.1, 1.5.0, 1.5.1, 1.6.0, 1.7.0, 1.7.1, 1.8.0, 1.9.0, 1.10.0, 1.10.1, 1.11.0, 1.12.0, 1.12.2, 1.12.3, 1.13.1, 1.13.2, 1.14.0, 1.15.0, 1.15.2, 1.15.3, 1.15.4, 1.15.5, 2.0.0, 2.0.1, 2.0.2, 2.0.3, 2.0.4, 2.1.0, 2.1.1, 2.1.2, 2.1.3, 2.1.4, 2.2.0, 2.2.1, 2.2.2, 2.2.3, 2.3.0, 2.3.1, 2.3.2, 2.3.3, 2.3.4, 2.4.0, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.5.0, 2.5.1, 2.5.2, 2.6.0, 2.6.1, 2.6.2)
ERROR: No matching distribution found for tensorflow-gpu==2.7.0
```

As pip 3.7 was not installed, the above error was triggered. 

Following the [stackoverflow link](https://stackoverflow.com/questions/54633657/how-to-install-pip-for-python-3-7-on-ubuntu-18), I executed the below

```
sudo apt install python3-pip
python3.7 -m pip install pip
```

Now I executed -> `$ pip install tensorflow-gpu==2.7.0` and tensorflow-gpu 2.7.0 was successfully installed. Yeah!!!!


