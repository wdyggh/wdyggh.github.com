---
layout: post
category: "embedded"
title: "[P]opencv-python_10"
tags: ["opencv","python","raspcam"]
---


### opencv-python_Canny

<a name="top"></a>




####在 OpenCV 中只需要一个函数： cv2.Canny()，就可以完成以上几步。让我们看如何使用这个函数。这个函数的第一个参数是输入图像。第二和第三个分别是 minVal 和 maxVal。第三个参数设置用来计算图像梯度的 Sobel卷积核的大小，默认值为 3。最后一个参数是 L2gradient，它可以用来设定求梯度大小的方程。如果设为 True，就会使用我们上面提到过的方程，否则使用方程： $$Edge−Gradient(G) = |G2 x| + |G2 y| $$ 代替，默认值为 False

- - -


```python
# -*- coding: utf-8 -*-

import cv2
import numpy as np
from matplotlib import pyplot as plt
img = cv2.imread('messi5.jpg',0)
edges = cv2.Canny(img,100,200)
plt.subplot(121),plt.imshow(img,cmap = 'gray')
plt.title('Original Image'), plt.xticks([]), plt.yticks([])
plt.subplot(122),plt.imshow(edges,cmap = 'gray')
plt.title('Edge Image'), plt.xticks([]), plt.yticks([])
plt.show()
```

- - - 

###[TOP](#top)
