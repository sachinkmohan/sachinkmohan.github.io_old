---
layout: post
title:  "github undoing the committed files"
date:   2022-01-17 16:00:00 +0200
last_modified_at: 2022-01-17 17:00:00 +0200
permalink: github-undoing-commit-files
description: github undoing the committed files and other hacks
published: true
sitemap: true
github_comments_issueid: "10"
categories: [github]  
---

`git diff --stat origin/master..` -> Gives the list of all the files from last commit 

`git log -2` -> gives list of last two commits


`git show your-commit-id --name-only` -> this will do the same as the above, get the `commit_id` from the above log 

`git reset --soft HEAD~1` -> Undo's your last commit, this is the most important thing if you did `git add .` or any other `git add file_name` accidentaly

`git diff --name-only` -> shows unstaged changes, i.e not committed files


#### Saw the below drawing in a stackoverflow [comment](https://stackoverflow.com/questions/35978550/how-to-show-uncommitted-changes-in-git-and-some-git-diffs-in-detail)

<img src="https://i.stack.imgur.com/Ev0z9.jpg" style="width: 40%; height: 40%"/>

