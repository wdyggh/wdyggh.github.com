---
layout: post
category: "opencv_python"
title: "[P]opencv-python_06"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>
###opencv-python_pixel



```python
# -*- coding: utf-8 -*-

import cv2
import numpy as np 

img=cv2.imread('lena.jpg')

'''
px=img[100,100]
print px
blue=img[100,100,0]
print blue
'''

'''
#修改像素值
img[100,100]=[255,255,255]
print img[100,100]
'''

'''
#获取像素值及修改
print img.item(10,10,2)
img.itemset((10,10,2),100)
print img.item(10,10,2)
'''

'''
#获取图像属性-行数,列数,通道数的元组。
#如果图像是灰度图，返回值仅有行数和列数
print img.shape
'''

'''
#图像的像素数目
print img.size
'''

'''
#图像的数据类型
print img.dtype
'''
'''
#----ROI----
#对一幅图像的特定区域进行操作
#现在我们选择球的部分并把他拷贝到图像的其他区域。
ball = img[280:340, 330:390]
img[273:333, 100:160] = ball
cv2.namedWindow('image', cv2.WINDOW_NORMAL)
cv2.imshow('image',img)
cv2.waitKey(0)
cv2.destroyAllWindow()
'''

#----拆分及合并图像通道----
#cv2.split() 是一个比较耗时的操作。只有真正需要时才用它，能用Numpy 索引就尽量用。
b,g,r=cv2.split(img)
img = cv2.merge((b,g,r))

#b=img[:,:,0]

#img[:,:,2]=0

cv2.imshow('image',img)
cv2.waitKey(0)
cv2.destroyAllWindow()


```



- - - 

###[TOP](#top)
