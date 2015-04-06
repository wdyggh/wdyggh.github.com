---
layout: post
category: "embedded"
title: "[P]opencv-python_05"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>
###opencv-python_trackbar
###物体追踪

* cv2.getTrackbarPos(), cv2.creatTrackbar()

- - - 

```python
import cv2
import numpy as np
def nothing(x):
	pass
# 创建一副黑色图像
img=np.zeros((300,512,3),np.uint8)
cv2.namedWindow('image')
cv2.createTrackbar('R','image',0,255,nothing)
cv2.createTrackbar('G','image',0,255,nothing)
cv2.createTrackbar('B','image',0,255,nothing)
#--------------------------------------------
switch='0:OFF\n1:ON'
#--------------------------------------------
cv2.createTrackbar(switch,'image',0,1,nothing)
while(1):
	cv2.imshow('image',img)
	k=cv2.waitKey(1)&0xFF
	if k==27:
		break
	r=cv2.getTrackbarPos('R','image')
	g=cv2.getTrackbarPos('G','image')
	b=cv2.getTrackbarPos('B','image')
	s=cv2.getTrackbarPos(switch,'image')
	if s==0:
		img[:]=0 	#黑色
		#img[:]=255 	#白色
	else:
		#img[:]=[b,g,r]
		img[:]=[r,g,b]
cv2.destroyAllWindows()
```

- - - 


```python
import cv2
import numpy as np
def nothing(x):
	pass
# 当鼠标按下时变为 True
drawing=False
# 如果 mode 为 true 绘制矩形。按下'm' 变成绘制曲线。
mode=True
ix,iy=-1,-1
global r,g,b,color
r,g,b=-1,-1,-1
color=(-1,-1,-1)
# 创建回调函数
def draw_circle(event,x,y,flags,param):
	'''
	#--------------------------------
	r=cv2.getTrackbarPos('R','image')
	g=cv2.getTrackbarPos('G','image')
	b=cv2.getTrackbarPos('B','image')
	'''
	#color=(b,g,r)
	#--------------------------------
	global ix,iy,drawing,mode
	# 当按下左键是返回起始位置坐标
	if event==cv2.EVENT_LBUTTONDOWN:
		drawing=True
		ix,iy=x,y
	# 当鼠标左键按下并移动是绘制图形。 event 可以查看移动， flag 查看是否按下
	elif event==cv2.EVENT_MOUSEMOVE and flags==cv2.EVENT_FLAG_LBUTTON:
		if drawing==True:
			if mode==True:
				cv2.rectangle(img,(ix,iy),(x,y),color,-1)
			else:
			# 绘制圆圈，小圆点连在一起就成了线， 3 代表了笔画的粗细
				cv2.circle(img,(x,y),3,color,-1)
			# 下面注释掉的代码是起始点为圆心，起点到终点为半径的
			# r=int(np.sqrt((x-ix)**2+(y-iy)**2))
			# cv2.circle(img,(x,y),r,(0,0,255),-1)
	# 当鼠标松开停止绘画。
	elif event==cv2.EVENT_LBUTTONUP:
		drawing==False
	# if mode==True:
	# cv2.rectangle(img,(ix,iy),(x,y),(0,255,0),-1)
	# else:
	# cv2.circle(img,(x,y),5,(0,0,255),-1)
img=np.zeros((512,512,3),np.uint8)
cv2.namedWindow('image')
cv2.createTrackbar('R','image',0,255,nothing)
cv2.createTrackbar('G','image',0,255,nothing)
cv2.createTrackbar('B','image',0,255,nothing)
cv2.setMouseCallback('image',draw_circle)

while(1):
	
	r=cv2.getTrackbarPos('R','image')
	g=cv2.getTrackbarPos('G','image')
	b=cv2.getTrackbarPos('B','image')
	color=(b,g,r)
	cv2.imshow('image',img)
	img[0:10]=255
	img[10:30]=color
	img[30:40]=255

	k=cv2.waitKey(1)&0xFF
	if k==ord('m'):
		mode=not mode
	elif k==27:
		break

```

- - - 

### 调整hsv 实现追踪相同颜色物体

```python
# -*- coding: utf-8 -*-

import cv2
import numpy as np
cap=cv2.VideoCapture(1)

def nothing(x):
	pass


cv2.namedWindow('image')
cv2.createTrackbar('h_max','image',179,179,nothing)
#cv2.createTrackbar('滑动条的名字','滑动条被放置窗口的名字',滑动条的默认位置,滑动条的最大值,回调函数)
cv2.createTrackbar('h_min','image',0,179,nothing)
cv2.createTrackbar('s_max','image',255,255,nothing)
cv2.createTrackbar('s_min','image',0,255,nothing)
cv2.createTrackbar('v_max','image',255,255,nothing)
cv2.createTrackbar('v_min','image',0,255,nothing)


while(1):
	# 获取每一帧
	ret,frame=cap.read()
	# 转换到 HSV
	hsv=cv2.cvtColor(frame,cv2.COLOR_BGR2HSV)
	# 设定蓝色的阈值
	h_max=cv2.getTrackbarPos('h_max','image')
	h_min=cv2.getTrackbarPos('h_min','image')
	s_max=cv2.getTrackbarPos('s_max','image')
	s_min=cv2.getTrackbarPos('s_min','image')
	v_max=cv2.getTrackbarPos('v_max','image')
	v_min=cv2.getTrackbarPos('v_min','image')
	#lower_blue=np.array([110,50,50])
	lower_blue=np.array([h_min,s_min,v_min])
	#upper_blue=np.array([130,255,255])
	upper_blue=np.array([h_max,s_max,v_max])
	
	# 根据阈值构建掩模
	mask=cv2.inRange(hsv,lower_blue,upper_blue)
	# 对原图像和掩模进行位运算
	res=cv2.bitwise_and(frame,frame,mask=mask)
	# 显示图像
	cv2.imshow('frame',frame)
	cv2.imshow('mask',mask)
	cv2.imshow('res',res)
	k=cv2.waitKey(5)&0xFF
	if k==27:
		break
# 关闭窗口
cv2.destroyAllWindows()
```

- - - 

###[TOP](#top)
