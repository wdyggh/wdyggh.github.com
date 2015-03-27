---
layout: post
category: "embedded"
title: "[P]opencv-python01"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>





> 必要函数 

```python
cv2.imread()
cv2.imshow()
cv2.imwrite()
```

### 01 载入图像

```python
# -*- coding: utf-8 -*-
import numpy as np
import cv2

img = cv2.imread('lena.jpg',0)
```

### 02 显示图像

```python
cv2.imshow('image',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
import numpy as np
import cv2
cv2.namedWindow('image', cv2.WINDOW_NORMAL)
cv2.imshow('image',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### 03保存图像

```python
cv2.imwrite('messigray.png',img)
```

```python
import numpy as np
import cv2
img = cv2.imread('messi5.jpg',0)
cv2.imshow('image',img)

k = cv2.waitKey(0)

if k == 27: # wait for ESC key to exit
	cv2.destroyAllWindows()
elif k == ord('s'): # wait for 's' key to save and exit
	cv2.imwrite('messigray.png',img)
	cv2.destroyAllWindows()
```

- - - 

###[TOP](#top)
