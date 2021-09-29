---
layout: post
title:  "Nvidia Jetson Xavier AGX Tensorflow(TF) Installation errors"
date:   2021-08-23 21:00:00 +0200
last_modified_at: 2021-08-30 18:30:00 +0200
permalink: nvidia-jetson-xavier-agx-tensorflow-installation-errors
description: How to install tensorflow on jetson AGX Xavier board. Fix errors while installing Tensorflow on jetson AGX board.
published: true
sitemap: true
categories: jetson nvidia agx-xavier
---
## Nvidia Jetson Xavier AGX Tensorflow(TF) Installation errors

- I followed the instructions to install tensorflow from this Nvidia standard documentation [link](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html)

 > Official TF for Xavier is found here [Link](https://forums.developer.nvidia.com/t/official-tensorflow-for-jetson-agx-xavier/65523) <br>

 > Find out the Jetpack version installed by this(not sure about this) -> `sudo apt show nvidia-jetpack` . Also can be found in sdkmanager while installing.
 
 > My output of the `sudo apt show nvidia-jetpack`
 ```
Package: nvidia-jetpack
Version: 4.5.1-b17
Priority: standard
Section: metapackages
Maintainer: NVIDIA Corporation
Installed-Size: 199 kB
Depends: nvidia-cuda (= 4.5.1-b17), nvidia-opencv (= 4.5.1-b17), nvidia-cudnn8 (= 4.5.1-b17), nvidia-tensorrt (= 4.5.1-b17), nvidia-visionworks (= 4.5.1-b17), nvidia-container (= 4.5.1-b17), nvidia-vpi (= 4.5.1-b17), nvidia-l4t-jetson-multimedia-api (>> 32.5-0), nvidia-l4t-jetson-multimedia-api (<< 32.6-0)
Homepage: http://developer.nvidia.com/jetson
Download-Size: 29,4 kB
APT-Manual-Installed: yes
APT-Sources: https://repo.download.nvidia.com/jetson/t194 r32.5/main arm64 Packages
Description: NVIDIA Jetpack Meta Package
 ```

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

> My PYTHONPATH in .bashrc file looks like this `export PYTHONPATH=/usr/local/lib/python3.6/dist-packages:$PYTHONPATH`

> Note: As your tensorflow and other ML related libraries are installed in `/usr/local/lib` instead of `/usr/lib`, this throws an error.


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
> So I fixed this error by flashing the whole jetson board, check my other post [link](), I did a fresh installation of tensorflow specifically for AGX, just google - you will get it. I also created a virtual environment and installed everything under it. I also installed jetpack using `sudo apt-get`. I made sure cuda is installed under `usr/local/cuda`

### Now I have a new error 

```
>>> import tensorflow
2021-08-26 18:27:42.470472: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.10.2
Traceback (most recent call last):
  File "/usr/local/lib/python3.6/dist-packages/tensorflow_core/python/pywrap_tensorflow.py", line 58, in <module>
    from tensorflow.python.pywrap_tensorflow_internal import *
  File "/usr/local/lib/python3.6/dist-packages/tensorflow_core/python/pywrap_tensorflow_internal.py", line 2449, in <module>
    from tensorflow.python.util import deprecation
  File "/usr/local/lib/python3.6/dist-packages/tensorflow_core/python/util/deprecation.py", line 26, in <module>
    from tensorflow.python.platform import tf_logging as logging
  File "/usr/local/lib/python3.6/dist-packages/tensorflow_core/python/platform/tf_logging.py", line 36, in <module>
    import six
ModuleNotFoundError: No module named 'six'

```
> _Fixed this error by installing six(which is a library for smoothing code compatibility b/w python 2 and 3)_ 
 
>`pip3 install six`

### I am trying to install [Tensorflow for Jetson](https://github.com/NVIDIA-AI-IOT/tf_trt_models)
- When I tried to install the script as below
`./install.sh python3`

I got the below error

```
You are attempting to install a package to a directory that is not
on PYTHONPATH and which Python does not read ".pth" files from.  The
installation directory you specified (via --install-dir, --prefix, or

the distutils default setting) was:

    /Users/user/.local/lib/python3.5/site-packages/

and your PYTHONPATH environment variable currently contains:

    '/usr/local/opt/opencv3/lib/python3.5/site-packages/'

Here are some of your options for correcting the problem:

* You can choose a different installation directory, i.e., one that is
  on PYTHONPATH or supports .pth files

* You can add the installation directory to the PYTHONPATH environment
  variable.  (It must then also be on PYTHONPATH whenever you run
  Python and want to use the package(s) you are installing.)

* You can set up the installation directory to support ".pth" files by
  using one of the approaches described here:

  https://setuptools.readthedocs.io/en/latest/easy_install.html#custom-installation-locations
```
**How to fix**
- I fixed this by updating my PYTHONPATH in .bashrc file to the below
`export PYTHONPATH=/usr/local/lib/python3.6/dist-packages:/home/agxdbot/.local/lib/python3.6/site-packages:$PYTHONPATH`

#### Another error while trying to install the `install.sh` script
```
Traceback (most recent call last):
  File "setup.py", line 17, in <module>
    from setuptools import find_packages
  File "/usr/local/lib/python3.6/dist-packages/setuptools/__init__.py", line 19, in <module>
    import setuptools.version
  File "/usr/local/lib/python3.6/dist-packages/setuptools/version.py", line 1, in <module>
    import pkg_resources
  File "/usr/local/lib/python3.6/dist-packages/pkg_resources/__init__.py", line 1380
    raise SyntaxError(e) from e
```

**How to fix**
setuptools is installed for lower version of TF. Jetson should suggest a newer ones while installing with TF 1.15 versions
Install a new version of setuptools from this [link](https://pypi.org/project/setuptools/#history)
> Note: type pip3 in the beginning for python3 installation.


##### Small update
> I installed TF 1.15
```
sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v45 tensorflow==v1.15.5
```
```
Successfully installed absl-py-0.13.0 astor-0.8.1 astunparse-1.6.3 dataclasses-0.8 gast-0.3.3 google-pasta-0.2.0 grpcio-1.40.0rc1 importlib-metadata-4.7.1 markdown-3.3.4 opt-einsum-3.3.0 tensorboard-1.15.0 tensorflow-1.15.5+nv21.6 tensorflow-estimator-1.15.1 termcolor-1.1.0 typing-extensions-3.10.0.0 werkzeug-2.0.1 wrapt-1.13.0rc3 zipp-3.5.0
```

## How to install  protobuf compiler 
- Download appropriate protobuf script from this [link](https://github.com/jkjung-avt/jetson_nano)
- Install protobuf compiler as told in step 10 of this [wonderful blog](https://www.pyimagesearch.com/2020/03/25/how-to-configure-your-nvidia-jetson-nano-for-computer-vision-and-deep-learning/)
- I ran the script `install_protobuf-3.8.0.sh` as I had TF 1.15 installed.
- Also if you are using virtual environment, refer to step 10 mentioned in the 2nd bullet point. Follow the instructions to install in the virtual environment seperately.

## Tensorflow Object Detection
#### Few useful links
- Blog by Gilbert Tanner -> [link](https://gilberttanner.com/blog/run-tensorflow-on-the-jetson-nano)

> Note, [this standard installation](https://gilberttanner.com/blog/creating-your-own-objectdetector) doesn't work as it is meant for x86 architectures. The problem I faced was with the installation of protobuf mentioned in this blog. 

- [This repository](https://github.com/jkjung-avt/tf_trt_models) is most forked from the [standard NVIDIA tf_trt_models repository](https://github.com/NVIDIA-AI-IOT/tf_trt_models)


### Required installation and errors
- Jupyter Notebook not installed in pip -> `pip3 install jupyterlab`
- `ModuleNotFoundError: No module named 'PIL'` -> solved by `pip3 install PILLOW`
- ModuleNotFoundError: No module named 'matplotlib' -> Install Matplotlib in pip3. Here we have 2 steps when compared to just pip installation
[pip3 matplotlib installation](https://bodo-schoenfeld.de/einfuehrung-in-matplotlib/)


### Some useful commmands
launching jupyterlab → jupyter-lab
