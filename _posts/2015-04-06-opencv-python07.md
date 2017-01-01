---
layout: post
category: "opencv_python"
title: "[P]opencv-python_07"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>
###opencv-python_Arithmetic Operations


* cv2.add()， cv2.addWeighted() 

###Arithmetic Operations on Images 图像的算术运算

`g (x) = (1 − α) * f0(x) + α * f1(x)`  
`α(0~1)`  
`dst = α · img1 + β · img2 + γ`  
\\(g (x) = (1 − α) * f0(x) + α * f1(x)\\)  
α(0~1)  
\\(dst = α · img1 + β · img2 + γ\\)  


- - - 

###合并2图像

```python
import cv2
import numpy as np

img1=cv2.imread('ml.png')
img2=cv2.imread('opencv_logo.jpg')
dst=cv2.addWeighted(img1,0.7,img2,0.3,0)
#	dst = 0.7 · img1 + 0.3 · img2 + 0

cv2.imshow('dst',dst)
cv2.waitKey(0)
cv2.destroyAllWindow()

```

- - - 

###合并2图像 透明部分不显示

```python
# -*- coding: utf-8 -*-

import cv2
import numpy as np

# Load two images
img1 = cv2.imread('messi5.jpg')
img2 = cv2.imread('opencv_logo.png')

# I want to put logo on top-left corner, So I create a ROI
rows,cols,channels = img2.shape
roi = img1[0:rows, 0:cols ]

# Now create a mask of logo and create its inverse mask also
img2gray = cv2.cvtColor(img2,cv2.COLOR_BGR2GRAY)
ret, mask = cv2.threshold(img2gray, 10, 255, cv2.THRESH_BINARY)
mask_inv = cv2.bitwise_not(mask)

# Now black-out the area of logo in ROI
# 取 roi 中与 mask 中不为零的值对应的像素的值，其他值为 0
# 注意这里必须有 mask=mask 或者 mask=mask_inv, 其中的 mask= 不能忽略
img1_bg = cv2.bitwise_and(roi,roi,mask = mask_inv)
# 取 roi 中与 mask_inv 中不为零的值对应的像素的值，其他值为 0。
# Take only region of logo from logo image.
img2_fg = cv2.bitwise_and(img2,img2,mask = mask)

# Put logo in ROI and modify the main image
dst = cv2.add(img1_bg,img2_fg)
img1[0:rows, 0:cols ] = dst

cv2.imshow('res',img1)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

- - - 

###[TOP](#top)
