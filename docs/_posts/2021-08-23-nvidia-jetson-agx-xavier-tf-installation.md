---
layout: post
title:  "Nvidia Jetson Xavier AGX Tensorflow(TF) Installation errors"
date:   2021-08-23 21:00:00 +0200
last_modified_at: 2021-08-23 21:00:00 +0200
permalink: nvidia-jetson-xavier-agx-tensorflow-installation-errors
description: How to install tensorflow on jetson AGX Xavier board. Fix errors while installing Tensorflow on jetson AGX board.
published: true
sitemap: true
categories: jetson nvidia agx-xavier
---

- I followed the instructions to install tensorflow from this Nvidia standard documentation [link](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html)

From this release note [link](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform-release-notes/tf-jetson-rel.html#tf-jetson-rel) , I chose the TF version to install and I installed TF 1.14 from this sheet.

- After successfully installing I got the below message

`Successfully installed tensorboard-1.14.0 tensorflow-estimator-1.14.0 tensorflow-gpu-1.14.0+nv19.10
`
- I got the below error while verifying the TF installation

```
import tensorflow
Traceback (most recent call last):
File “”, line 1, in
ModuleNotFoundError: No module named ‘tensorflow’
```
I tried all the fix from these Nvidia forums [link1](https://forums.developer.nvidia.com/t/successful-installation-of-tensorflow-but-says-module-not-found-in-verification/80231) [link2](https://forums.developer.nvidia.com/t/tensorflow-intallation-failing-on-xavier/80159#5374834) [link3](https://forums.developer.nvidia.com/t/importerror-no-module-named-tensorflow-but-requirement-already-satisfied/154251)

These linked pointed out to one problem that my `PYTHONPATH` was not set in `.bashrc` file

- After setting that I tested if TF was installed properly using this command `pip3 show tensorflow-gpu`
 ```
 WARNING: pip is being invoked by an old script wrapper. This will fail in a future version of pip.
Please see https://github.com/pypa/pip/issues/5599 for advice on fixing the underlying issue.
To avoid this problem you can invoke Python with '-m pip' instead of running pip directly.
Name: tensorflow-gpu
Version: 1.14.0+nv19.10
Summary: TensorFlow is an open source machine learning framework for everyone.
Home-page: https://www.tensorflow.org/
Author: Google Inc.
Author-email: packages@tensorflow.org
License: Apache 2.0
Location: /usr/local/lib/python3.6/dist-packages
Requires: keras-preprocessing, numpy, wrapt, astor, keras-applications, gast, tensorflow-estimator, protobuf, wheel, termcolor, six, google-pasta, grpcio, absl-py, tensorboard
Required-by:
```
- But the actual problem comes when I type this on the terminal

```
(tf114) home:~$ python3
Python 3.6.9 (default, Jan 26 2021, 15:33:00) 
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow
Traceback (most recent call last):
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/pywrap_tensorflow.py", line 58, in <module>
    from tensorflow.python.pywrap_tensorflow_internal import *
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/pywrap_tensorflow_internal.py", line 28, in <module>
    _pywrap_tensorflow_internal = swig_import_helper()
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/pywrap_tensorflow_internal.py", line 24, in swig_import_helper
    _mod = imp.load_module('_pywrap_tensorflow_internal', fp, pathname, description)
  File "/usr/lib/python3.6/imp.py", line 243, in load_module
    return load_dynamic(name, filename, file)
  File "/usr/lib/python3.6/imp.py", line 343, in load_dynamic
    return _load(spec)
ImportError: libnvToolsExt.so.1: cannot open shared object file: No such file or directory

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/__init__.py", line 28, in <module>
    from tensorflow.python import pywrap_tensorflow  # pylint: disable=unused-import
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/__init__.py", line 49, in <module>
    from tensorflow.python import pywrap_tensorflow
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/pywrap_tensorflow.py", line 74, in <module>
    raise ImportError(msg)
ImportError: Traceback (most recent call last):
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/pywrap_tensorflow.py", line 58, in <module>
    from tensorflow.python.pywrap_tensorflow_internal import *
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/pywrap_tensorflow_internal.py", line 28, in <module>
    _pywrap_tensorflow_internal = swig_import_helper()
  File "/usr/local/lib/python3.6/dist-packages/tensorflow/python/pywrap_tensorflow_internal.py", line 24, in swig_import_helper
    _mod = imp.load_module('_pywrap_tensorflow_internal', fp, pathname, description)
  File "/usr/lib/python3.6/imp.py", line 243, in load_module
    return load_dynamic(name, filename, file)
  File "/usr/lib/python3.6/imp.py", line 343, in load_dynamic
    return _load(spec)
ImportError: libnvToolsExt.so.1: cannot open shared object file: No such file or directory


Failed to load the native TensorFlow runtime.

See https://www.tensorflow.org/install/errors

for some common reasons and solutions.  Include the entire stack trace
above this error message when asking for help.
```
**This error is pointing to Cuda installation. Unable to find cuda installation in the jetson board. Stuck here, need to find out how to proceed further**
_One thought is to install Cuda using SDK manager_
