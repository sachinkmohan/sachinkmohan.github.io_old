---
layout: post
title:  "The only github commands you ever need"
date:   2022-01-25 13:00:00 +0200
last_modified_at: 2022-01-25 14:00:00 +0200
permalink: only-github-commands
description: What are the only github commands you ever need. The most used github commands
published: true
sitemap: true
categories: [github, essentials]  
---

These are the github commands that I started with and I would like to share the same with you.

- `git init` -> to initialize a github repository
- `git add .` -> adds all the files to be committed
- `git commit -m "the reason of the commit"` -commits the files ready to be pushed
- `git push -u origin branch_name` -> pushes the files to the repository


#### Ignore hidden files

```
.*
!/.gitignore
```
[1]


### Advanced commands - Don't attempt these, if you are a git beginner

`git rm -r --cached .` -> This removes the index but the files resides on the local disk. It is important when you add files in `.gitignore`
and is not updated. [2]

### References
[1](https://stackoverflow.com/questions/8021441/how-to-ignore-all-hidden-directories-files-recursively-in-a-git-repository)
[2](https://stackoverflow.com/questions/5798930/git-rm-cached-x-vs-git-reset-head-x#:~:text=Whether%20git%20add%20was%20used,from%20the%20tree%20as%20well.)

