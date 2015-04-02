---
layout: post
category: "embedded"
title: "[P]opencv-python_03"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>
###opencv-python_drawingFunctions



• img：你想要绘制图形的那幅图像。
• color：形状的颜色。以 RGB 为例，需要传入一个元组，例如： （255,0,0）
代表蓝色。对于灰度图只需要传入灰度值。
• thickness：线条的粗细。如果给一个闭合图形设置为 -1，那么这个图形
就会被填充。默认值是 1.
• linetype：线条的类型， 8 连接，抗锯齿等。默认情况是 8 连接。 cv2.LINE_AA
为抗锯齿，这样看起来会非常平滑。

```python
# -*- coding: utf-8 -*-

import numpy as np
import cv2
# Create a black image
#img = cv2.imread('lena.jpg')
img=np.zeros((512,512,3), np.uint8)
# Draw a diagonal blue line with thickness of 5 px

# 画线  
cv2.line(img,(0,0),(511,511),(255,0,0),5)
#cv2.line(img,(起点坐标),(终点坐标),(RGB颜色),线条粗细)

#画矩形
cv2.rectangle(img,(0,0),(100,100),(0,255,0),1)
#cv2.rectangle(img,(左上角顶点),(右下角顶点的坐标),(RGB颜色),线条粗细 -1 是填充颜色)

#画圆
cv2.circle(img,(150,150), 50, (0,255,0), 1)
cv2.circle(img,(150,300), 50, (0,255,0), -1)
#cv2.circle(img,(圆形的中心点坐标), 半径, (RGB颜色), -1 是填充颜色)

#画椭圆
cv2.ellipse(img,(256,256),(100,50),0,0,180,255,-1)
#cv2.ellipse(img,(256,256),(100,50),0,0,180,255,-1)
#画椭圆比较复杂，我们要多输入几个参数。一个参数是中心点的位置坐标.下一个参数是长轴和短轴的长度。椭圆沿逆时针方向旋转的角度。椭圆弧演顺时针方向起始的角度和结束角度，如果是 0 很 360，就是整个椭圆。查看cv2.ellipse() 可以得到更多信息。下面的例子是在图片的中心绘制半个椭圆。

#画多边形
#pts=np.array([[10,5],[20,30],[70,20],[50,10]], np.int32)
#pts=pts.reshape((-1,1,2))

#添加文字
font=cv2.FONT_HERSHEY_SIMPLEX	#字体
cv2.putText(img,'OpenCV',(10,400), font, 2,(255,255,255),9)
#cv2.putText(img,'添加的文字',(起点坐标), 字体, 字体大小,(颜色),线条粗细)


cv2.imshow('image',img)
cv2.waitKey(0)
cv2.destroyAllWindows()


```


- - - 

###[TOP](#top)
