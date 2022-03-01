---
layout: post
title:  "How to move your most recent file from Downloads to your current working directory"
date:   2022-01-22 16:00:00 +0200
last_modified_at: 2022-01-22 15:00:00 +0200
permalink: move-file-linux
description: How to move your most recent file from Downloads to your current working directory
published: true
sitemap: true
categories: [linux]
---
How  many times did you have to navigate to the Downloads folder and move the file to your target directory. 
Well, I am tired doing it, so automating it.

1. Create a bash script, in my case I named it to `mvd`
    - paste the following [1] 
```
#!/bin/sh
filename=$(find /home/mohan/Downloads -type f -printf "%T@ %p\n" | sort -n | cut -d' ' -f 2- | tail -n 1)
mv $filename .
```

2. Give execute permission to the file `chmod +x mvd`
3. Add the location containing this script to the `.bashrc` file -> `export PATH=$PATH:/home/user/yourfoldername/` so that you can basically call it from anywhere.

That's it folks! Enjoy! 

#### Ref
----
[1](https://stackoverflow.com/questions/1015678/get-most-recent-file-in-a-directory-on-linux)
