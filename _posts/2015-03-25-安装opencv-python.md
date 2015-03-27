---
layout: post
category: "embedded"
title: "[P]Install opencv-python on RaspberryPi"
tags: ["raspberrypi","python","opencv"]
---

<a name="top"></a>
#Install opencv-python & opencv on RaspberryPi




## Install opencv-python

`based on python`

```bash
apt-get install livopencv-dev
apt-get install python-opencv
```

在命令行中 输入`python` 加载 `import cv2`  判定安装是否成功


## Install opencv

* 安装必要的packages

> GCC 4.4.x or later  
> CMake 2.8.7 or higher  
> Git  
> GTK+2.x or higher, including headers (libgtk2.0-dev)  
> pkg-config  
> Python 2.6 or later and Numpy 1.5 or later with developer packages (python-dev, python-numpy)  
> ffmpeg or libav development packages: libavcodec-dev, libavformat-dev, libswscale-dev  
> [optional] libtbb2 libtbb-dev  
> [optional] libdc1394 2.x  
> [optional] libjpeg-dev, libpng-dev, libtiff-dev, libjasper-dev, libdc1394-22-dev  

```bash
[compiler] sudo apt-get install build-essential
[required] sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
[optional] sudo apt-get install python-dev python-numpy libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```

* 从github仓库获取代码

```bash
git clone https://github.com/Itseez/opencv.git
git clone https://github.com/Itseez/opencv_contrib.git
```

* 配置cmake

```bash
cmake -D OPENCV_EXTRA_MODULES_PATH=/opencv_contrib/modules/的目录 CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
```

* 接下来,这一步需要很长时间

```bash
make
```

* 然后

```bash
make install
```



- - - 

###[TOP](#top)
