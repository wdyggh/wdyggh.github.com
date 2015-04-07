---
layout: post
category: "embedded"
title: "[P]opencv-python_08"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>
###opencv-python_GeometricTransformations



对图像进行各种几个变换，例如移动，旋转，仿射变换等

* cv2.getPerspectiveTransform

###OpenCV 提供了两个变换函数， cv2.warpAffine 和 cv2.warpPerspective，使用这两个函数你可以实现所有类型的变换。 cv2.warpAffine 接收的参数是2 × 3 的变换矩阵，而 cv2.warpPerspective 接收的参数是 3 × 3 的变换矩阵。

###扩展缩放

```python
import cv2
import numpy as np
img=cv2.imread('messi5.jpg')
# 下面的 None 本应该是输出图像的尺寸，但是因为后边我们设置了缩放因子
# 因此这里为 None
res=cv2.resize(img,None,fx=2,fy=2,interpolation=cv2.INTER_CUBIC)
#OR
# 这里呢，我们直接设置输出图像的尺寸，所以不用设置缩放因子
height,width=img.shape[:2]
res=cv2.resize(img,(2*width,2*height),interpolation=cv2.INTER_CUBIC)
while(1):
	cv2.imshow('res',res)
	cv2.imshow('img',img)
	if cv2.waitKey(1) & 0xFF == 27:
		break
cv2.destroyAllWindows()
```

- - - 

###平移

```python
import cv2
import numpy as np

img = cv2.imread('messi5.jpg',0)
rows,cols = img.shape

M = np.float32([[1,0,100],[0,1,50]])
#M = np.float32([[1,0,shift_x],[0,1,shift_y]])
dst = cv2.warpAffine(img,M,(cols,rows))

cv2.imshow('img',dst)
cv2.waitKey(0)
cv2.destroyAllWindows()

```

- - - 

###旋转

```python
# -*- coding: utf-8 -*-

import cv2
import numpy as np
img=cv2.imread('messi5.jpg',0)
rows,cols=img.shape
# 这里的第一个参数为旋转中心，第二个为旋转角度，第三个为旋转后的缩放因子
# 可以通过设置旋转中心，缩放因子，以及窗口大小来防止旋转后超出边界的问题
M=cv2.getRotationMatrix2D((cols/2,rows/2),90,0.6)
# 第三个参数是输出图像的尺寸中心
dst=cv2.warpAffine(img,M,(2*cols,2*rows))
while(1):
	cv2.imshow('img',dst)
	if cv2.waitKey(1)&0xFF==27:
		break
cv2.destroyAllWindows()
```

###仿射变换

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt
img=cv2.imread('drawing.jpg')
rows,cols,ch=img.shape
pts1=np.float32([[50,50],[200,50],[50,200]])
pts2=np.float32([[10,100],[200,50],[100,250]])
M=cv2.getAffineTransform(pts1,pts2)
dst=cv2.warpAffine(img,M,(cols,rows))
plt.subplot(121,plt.imshow(img),plt.title('Input'))
plt.subplot(121,plt.imshow(img),plt.title('Output'))
plt.show()
```


###透视变换

```python

import cv2
import numpy as np
from matplotlib import pyplot as plt
img=cv2.imread('sudokusmall.png')
rows,cols,ch=img.shape
pts1 = np.float32([[56,65],[368,52],[28,387],[389,390]])
pts2 = np.float32([[0,0],[300,0],[0,300],[300,300]])
M=cv2.getPerspectiveTransform(pts1,pts2)
dst=cv2.warpPerspective(img,M,(300,300))
plt.subplot(121,plt.imshow(img),plt.title('Input'))
plt.subplot(121,plt.imshow(img),plt.title('Output'))
plt.show()
```

- - - 

###[TOP](#top)
