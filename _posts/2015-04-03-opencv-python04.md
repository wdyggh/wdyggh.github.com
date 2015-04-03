---
layout: post
category: "embedded"
title: "[P]opencv-python_04"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>
###opencv-python_mousePaint


* cv2.setMouseCallback()

```python

# -*- coding: utf-8 -*-


import cv2
import numpy as np
#mouse callback function
def draw_circle(event,x,y,flags,param):
	if event==cv2.EVENT_LBUTTONDBLCLK:
	#在双击过的地方绘制一个圆圈
		cv2.circle(img,(x,y),100,(255,0,0),-1)

# 创建图像与窗口并将窗口与回调函数绑定
img=np.zeros((512,512,3),np.uint8)
cv2.namedWindow('image')
cv2.setMouseCallback('image',draw_circle)

while(1):
	cv2.imshow('image',img)
	if cv2.waitKey(20)&0xFF==27:
		break
cv2.destroyAllWindows()
```


* 鼠标按下的状态下 不停的画矩形，圆  不是想象中从鼠标按下的坐标到弹起的坐标画的一个矩形或圆

```python

import cv2
import numpy as np
# 当鼠标按下时变为 True
drawing=False
# 如果 mode 为 true 绘制矩形。按下'm' 变成绘制曲线。
mode=True
ix,iy=-1,-1
# 创建回调函数
def draw_circle(event,x,y,flags,param):
	global ix,iy,drawing,mode
	if event==cv2.EVENT_LBUTTONDOWN:
	#鼠标左键按下  此时的x,y坐标
		drawing=True
		ix,iy=x,y
	elif event==cv2.EVENT_MOUSEMOVE and flags==cv2.EVENT_FLAG_LBUTTON:
	#鼠标移动&左键按下状态
		if drawing==True:
			if mode==True:
			#画矩形
				cv2.rectangle(img,(ix,iy),(x,y),(0,255,0),1)
			else:
			#画圆
				cv2.circle(img,(x,y),3,(0,0,255),-1)
			# 下面注释掉的代码是起始点为圆心，起点到终点为半径的
			# r=int(np.sqrt((x-ix)**2+(y-iy)**2))
			# cv2.circle(img,(x,y),r,(0,0,255),-1)
			# 当鼠标松开停止绘画。
	elif event==cv2.EVENT_LBUTTONUP:
	#鼠标松开
		drawing==False
	# if mode==True:
	# cv2.rectangle(img,(ix,iy),(x,y),(0,255,0),-1)
	# else:
	# cv2.circle(img,(x,y),5,(0,0,255),-1)

img=np.zeros((512,512,3),np.uint8)
cv2.namedWindow('image')
cv2.setMouseCallback('image',draw_circle)

while(1):
	cv2.imshow('image',img)
	k=cv2.waitKey(1)&0xFF
	if k==ord('m'):
		mode=not mode
	elif k==27:
		break

cv2.destroyAllWindows()

```


- - - 

###[TOP](#top)
