---
aliases:
- /rpi4/pytorch/2020/06/30/pytorch-raspberry
categories:
- rpi4
- pytorch
date: '2020-06-30'
layout: post
title: Installing Pytorch on a raspberry pi 4

---

# Update 15 sept 2020 
I found [these wheel builds](https://mathinf.com/pytorch/arm64/) from [Thomas Viehmann](https://twitter.com/ThomasViehmann/status/1302944934333382656) that worked very well on a rpi4 64 bit running python 3.7. They are **pytorch 1.6.0** and avoids the original hacks.
Only issue was that my camera stopped working, but manage to circumvent it by using a different driver (v4l-utils) and using opencv's VideoCapture() to get images. 
Got it running in a docker image with the following (removed some parts that I dont think is necessary):

(the balena docker image is a fairly stripped down ubuntu image)

```
FROM balenalib/raspberrypi4-64:latest
# Defines our working directory in container
WORKDIR /usr/src/app
RUN sudo apt-get update
RUN apt-get install -y gcc python3-dev v4l-utils python3-opencv python3-pip python3-setuptools libffi-dev libssl-dev

# PYTORCH: 
RUN wget https://mathinf.com/pytorch/arm64/torch-1.6.0a0+b31f58d-cp37-cp37m-linux_aarch64.whl
RUN wget https://mathinf.com/pytorch/arm64/torchvision-0.7.0a0+78ed10c-cp37-cp37m-linux_aarch64.whl
RUN sudo apt-get install -y python3-numpy python3-wheel python3-setuptools python3-future python3-yaml python3-six python3-requests python3-pip python3-pillow
RUN pip3 install torch*.whl torchvision*.whl
```


# Original Post
Earlier this year I had to install pytorch on a raspiberry pi for my robotic lawn mower project (more on that later). However, the process was _very_ painful, so Ill throw my notes here in case anyone else tries to do the same. Its not supposed to be bullet-proof, but may help with some pointers. Updates to this proceudre may be found [here](https://github.com/simeneide/gardengoat#torch-and-torchvision).

Installed from wheel on these:
https://github.com/nmilosev/pytorch-arm-builds

But for rpi4 there was some errors, so I installed a wheel after reading this comment:
https://github.com/nmilosev/pytorch-arm-builds/issues/4#issuecomment-527433112

Install from his wheel a bit longer down the thread, and rename those _C.**.so and _d.**.so files to _C.so and _d.so.

Torchvision works, but Pillow 7.0.0 was too new, so downgraded to 6.1 after some random comments I found.


## Step-by-step:

### PIP install pytorch from wheel
Download wheel from here `https://github.com/nmilosev/pytorch-arm-builds` and run `sudo pip3 install torch-1.1.0-cp37-cp37m-linux_armv7l.whl`

### Rename some files
Then if you try to run `sudo python3 -c "import torch"` you get:

```
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/usr/local/lib/python3.7/dist-packages/torch/__init__.py", line 79, in <module>
    from torch._C import *
ModuleNotFoundError: No module named 'torch._C'
```
Can be fixed by the following:
```
cd /usr/local/lib/python3.7/dist-packages/torch
sudo mv _C.cpython-37m-arm-linux-gnueabi.so _C.so
sudo mv _dl.cpython-37m-arm-linux-gnueabi.so _dl.so
```
