---
layout: post
category: "embedded"
title: "[P]opencv-python_11"
tags: ["opencv","python","raspcam"]
---


###opencv-python_contours
<a name="top"></a>


####OpenCV 中的轮廓

- - -


```python
# -*- coding: utf-8 -*-
#OpenCV 中的轮廓
import numpy as np
import cv2

im = cv2.imread('4.jpg')
cv2.imshow("original image",im)
imgray = cv2.cvtColor(im,cv2.COLOR_BGR2GRAY)
ret,thresh = cv2.threshold(imgray,100,255,0)	#简单阈值
#ret,结果图像 = cv2.threshold(原图像,对像素值进行分类的阈值 ,新的像素值, 多种不同的阈值方法)
image,contours, hierarchy = cv2.findContours(thresh,cv2.RETR_TREE,cv2.CHAIN_APPROX_SIMPLE)	#找轮廓
#图像,轮廓,轮廓的层析结构=cv2.findContours(输入图像,轮廓检索模式,轮廓近似方法)
img=cv2.drawContours(im,contours,0,(0,255,0),3)	#绘制轮廓
#img = cv2.drawContour(原始图像, 轮廓, 轮廓的索引, 轮廓的颜色, 厚度)

cv2.imshow('img',img)
cv2.waitKey(0) ## Wait for keystroke
cv2.destroyAllWindows() ## Destroy all windows﻿


```
 
- - -
 
####轮廓特征

```python
# -*- coding: utf-8 -*-

import cv2
import numpy as np

img = cv2.imread('4.jpg',0)
ret,thresh = cv2.threshold(img,127,255,0)
image,contours,hierarchy = cv2.findContours(thresh, 1, 2)

cnt = contours[0]
M = cv2.moments(cnt)
print M	#矩


area = cv2.contourArea(cnt)
print area 		#轮廓面积

perimeter = cv2.arcLength(cnt,True)
print perimeter	#轮廓周长

epsilon = 0.1*cv2.arcLength(cnt,True)
approx = cv2.approxPolyDP(cnt,epsilon,True)
print approx 	#轮廓近似

```


- - - 

###[TOP](#top)
