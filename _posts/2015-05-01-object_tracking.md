---
layout: post
category: "embedded"
title: "[P]Object Tracking with opencv-python"
tags: ["opencv","python","tracking"]
---

<a name="top"></a>
###Object Tracking


- - -


```python
# -*- coding: utf-8 -*-

#Import OpenCV
import cv2
#Import Numpy
import numpy as np

camera_feed = cv2.VideoCapture(1)

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

    _,frame = camera_feed.read()
    #Convert the current frame to HSV
    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

    # 设定蓝色的阈值
    h_max=cv2.getTrackbarPos('h_max','image')
    h_min=cv2.getTrackbarPos('h_min','image')
    s_max=cv2.getTrackbarPos('s_max','image')
    s_min=cv2.getTrackbarPos('s_min','image')
    v_max=cv2.getTrackbarPos('v_max','image')
    v_min=cv2.getTrackbarPos('v_min','image')
    
    # -----------------pink------------------
    #lower_blue=np.array([110,50,50])
    lower_blue=np.array([h_min,s_min,v_min])
    #upper_blue=np.array([130,255,255])
    upper_blue=np.array([h_max,s_max,v_max])
    
    
    '''
    #Define the threshold for finding a blue object with hsv
    lower_blue = np.array([120,69,0])
    upper_blue = np.array([179,224,255])
    '''
    #Create a binary image, where anything blue appears white and everything else is black
    mask = cv2.inRange(hsv, lower_blue, upper_blue)
    res=cv2.bitwise_and(frame,frame,mask=mask)
    #Get rid of background noise using erosion and fill in the holes using dilation and erode the final image on last time
    element = cv2.getStructuringElement(cv2.MORPH_RECT,(9,9))
    mask = cv2.erode(mask,element, iterations=2)
    #cv2.erode() 图像的腐蚀运算 9*9的正方形卷积核 根据卷积核的大小 靠近前景的所有像素都会被腐蚀掉（变为 0），所以前景物体会变小，整幅图像的白色区域会减少。这对于去除白噪声很有用，也可以用来断开两个连在一块的物体等。
    mask = cv2.dilate(mask,element,iterations=2)
    #cv2.dilate() 图像的膨胀运算 与腐蚀相反，与卷积核对应的原图像的像素值中只要有一个是 1，中心元素的像素值就是 1。所以这个操作会增加图像中的白色区域（前景）。一般在去噪声时先用腐蚀再用膨胀。因为腐蚀在去掉白噪声的同时，也会使前景对象变小。所以我们再对他进行膨胀。这时噪声已经被去除了，不会再回来了，但是前景还在并会增加。膨胀也可以用来连接两个分开的物体。
    mask = cv2.erode(mask,element)
    
    #Create Contours for all blue objects
    image1,contours, hierarchy = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    #cv2.findContours() 在一个二值图像中查找轮廓 有三个输入参数，第一个是输入图像，第二个是轮廓检索模式，第三个是轮廓近似方法。返回值有三个，第一个是图像，第二个是轮廓，第三个是（轮廓的）层析结构。轮廓（第二个返回值）是一个 Python列表，其中存储这图像中的所有轮廓。每一个轮廓都是一个 Numpy 数组，包含对象边界点（x， y）的坐标。
    #image1,contours, hierarchy = cv2.findContours(mask, 1, 2)
    maximumArea = 0
    bestContour = None

    # for all object
    for contour in contours:
        '''
        #Straight Bounding Rectangle
        x,y,w,h = cv2.boundingRect(contour)
        cv2.rectangle(frame, (x,y),(x+w,y+h), (0,0,255), 3)
        '''

        #Rotated Rectangle
        rect = cv2.minAreaRect(contour)
        box = cv2.boxPoints(rect)
        box = np.int0(box)
        cv2.drawContours(frame,[box],0,(0,0,255),2)


    '''
    #only for the biggest object
    for contour in contours:
        currentArea = cv2.contourArea(contour)
        if currentArea > maximumArea:
            bestContour = contour
            maximumArea = currentArea
     #Create a bounding box around the biggest blue object
    if bestContour is not None:
        x,y,w,h = cv2.boundingRect(bestContour)
        cv2.rectangle(frame, (x,y),(x+w,y+h), (0,0,255), 3)
    '''

    #Show the original camera feed with a bounding box overlayed 
    cv2.imshow('frame',frame)

    #Show the contours in a seperate window
    #cv2.imshow('mask',mask)

    cv2.imshow('res',res)
    #Use this command to prevent freezes in the feed
    k = cv2.waitKey(5) & 0xFF
    #If escape is pressed close all windows
    if k == 27:
        break


cv2.destroyAllWindows() 
```

![objecttracking_trackbar](http://7xifyp.com1.z0.glb.clouddn.com/objecttracking_trackbar.JPG)

![objecttracking_res](http://7xifyp.com1.z0.glb.clouddn.com/objecttracking_res.JPG)

![objecttracking_frame](http://7xifyp.com1.z0.glb.clouddn.com/objecttracking_frame.JPG)


- - - 

###[TOP](#top)
