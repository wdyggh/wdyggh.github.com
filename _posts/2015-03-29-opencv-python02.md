---
layout: post
category: "embedded"
title: "[P]opencv-python_video"
tags: ["opencv","python","raspcam"]
---

<a name="top"></a>




```python
# -*- coding: utf-8 -*-
#从树莓派摄像头捕获视频
import numpy as np
import cv2
cap = cv2.VideoCapture(1)
#cv2.VideoCapture(1) 1:FOR RASPICAM

print ('video = %d*%d') %(cap.get(3),cap.get(4))

while(True):
	# Capture frame-by-frame
	ret, frame = cap.read()
	# Our operations on the frame come here
	gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
	# Display the resulting frame
	cv2.imshow('frame',gray)
	#cv2.imshow('frame1',frame)
	#For Colour Video
	if cv2.waitKey(1) & 0xFF == ord('q'):
		break
# When everything done, release the capture
cap.release()
cv2.destroyAllWindows()
```

- - -


```python
#播放本地视频文件
import numpy as np
import cv2

cap = cv2.VideoCapture('vtest.avi')

while(cap.isOpened()):
    ret, frame = cap.read()

    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    cv2.imshow('frame',gray)
    #灰度
    #cv2.imshow('frame',frame)
    #彩色
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

- - - 

```python
#录制视频到本地
import numpy as np
import cv2
cap = cv2.VideoCapture(1)
# Define the codec and create VideoWriter object
fourcc = cv2.VideoWriter_fourcc(*'XVID')
out = cv2.VideoWriter('output.avi',fourcc, 20.0, (640,480))
while(cap.isOpened()):
	ret, frame = cap.read()
	if ret==True:
		frame = cv2.flip(frame,0)
		# write the flipped frame
		out.write(frame)
		cv2.imshow('frame',frame)
		if cv2.waitKey(1) & 0xFF == ord('q'):
			break
	else:
		break
# Release everything if job is finished
cap.release()
out.release()
cv2.destroyAllWindows()
```

- - - 

###[TOP](#top)
