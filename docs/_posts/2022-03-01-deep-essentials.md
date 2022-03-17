---
layout: post
title:  "Deep learning cheat sheet"
date:   2022-03-01 16:00:00 +0200
last_modified_at: 2022-03-01 16:00:00 +0200
permalink: deep-learning-essentials
description: All useful tools for deep learning
published: true
sitemap: true
categories: cheat-sheet  
---

**1. How to compare 2 numpy arrays online**

There are no reliable online tools. 2 options. One is in python, other is in pycharm. I wanna explain about the latter. 
Load the numpy array using `np.load` and then hit the debug mode in pycharm. View the variable you loaded as array in pycharm and then export it to csv files. 
Then use any online csv compare tool to compare the arrays

**2. View the inputs and outputs of a frozen_graph**

- Replace `graph_inputs` by `graph_outputs` to print the outputs

```
import graphsurgeon as gs
graph = gs.DynamicGraph('./mask_rcnn_inception_v2_coco_2018_01_28/frozen_inference_graph.pb')

print(graph.graph_inputs)
```

Make sure to install `pip install graphsurgeon`

**3. Freeze all the packages in your pip environment to the requirements.txt** ➡️
`pip3 freeze > requirements.txt`

**4. Adding frame rate or fps to the opencv frames**
- https://learnopencv.com/how-to-find-frame-rate-or-frames-per-second-fps-in-opencv-python-cpp/
