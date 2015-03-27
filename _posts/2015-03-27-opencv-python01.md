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

img = cv2.imread('messi5.jpg',0)
```

- - - 

###[TOP](#top)
