---
layout: post
title:  "Essential virtual environment tools"
date:   2022-01-22 10:00:00 +0200
last_modified_at: 2022-01-22 11:00:00 +0200
permalink: essential-venv-tools
description: What are the essential virtual environment tools required in a pip or conda environment
published: true
sitemap: true
categories: [cheat-sheet]
---

**1. Jupyter notebook - Who can live without it?** - [Ref.](https://jupyter.org/install)
```
pip install notebook
jupyter notebook
```
Using conda it will be 
```
conda install -c anaconda jupyter
```

**2. conda most used commands**

```python
conda create --name envname python=3.5
conda env remove --name bio-env  
```
