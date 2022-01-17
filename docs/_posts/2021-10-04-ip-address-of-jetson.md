---
layout: post
title:  "Finding IP address of the jetson board without serial port or additional display"
date:   2021-10-04 14:00:00 +0200
last_modified_at: 2021-10-04 14:02:00 +0200
permalink: how-find-IP-address-of-the-jetson-board
description: How to find the IP address of the jetson board
published: true
sitemap: true
github_comments_issueid: "4"
categories: [jetson, nvidia, agx-xavier]
---

We will be using a tool called Nmap, which can be installed in ubuntu.

1. Before connecting the jetson board run the command `nmap -sn X.X.X.X/Y`, which will return all the IP's in the system. 
2. Now connect the jetson board and run again `nmap -sn X.X.X.X/Y`, if a new IP is assigned, you will find it now. 

What I did, 
- I ran the above command and saved it to a file `nmap -sn X.X.X.X/Y > file1.txt`
- Ran again after connecting the jetson board `nmap -sn X.X.X.X/Y > file2.txt`
- `vim -d file1.txt file2.txt`
This will show you the difference in the files side by side.

Note: Sometimes, you will get more than 1 IP after connecting the jetson board. You will have to give a trial and error method in that case. But this is not painful
as connecting your board to a display and a keyboard just to find it's IP. Thanks Dennis(RRLAB) for suggesting this easy hack!!

