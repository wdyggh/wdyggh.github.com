---
layout: post
category: "embedded"
title: "[P]Install opencv-python on RaspberryPi"
tags: ["raspberrypi","python","opencv"]
---

<a name="top"></a>
##Install opencv-python & opencv on RaspberryPi


`based on python`


* install opencv-python

```bash
apt-get install livopencv-dev
apt-get install python-opencv
```

在命令行中 输入`python` 加载 `import cv2`  判定安装是否成功


* install opencv

从github仓库获取代码

```bash
git clone https://github.com/Itseez/opencv.git
git clone https://github.com/Itseez/opencv_contrib.git
```

配置cmake

```bash
cmake -D OPENCV_EXTRA_MODULES_PATH=/opencv_contrib/modules/的目录 CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
```

接下来,这一步需要很长时间

```bash
make
```

然后

```bash
make install
```



- - - 

###[TOP](#top)
