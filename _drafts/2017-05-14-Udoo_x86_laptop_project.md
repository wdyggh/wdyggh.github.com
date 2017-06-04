---
layout: post
category: "UDOO_X86"
title: "UDOO x86 laptop project"
tags: ["laptop","udoo_x86"]
---

### A project based on UDOO x86 board  
{: #top}

Hello everyone!  
This an process about how I built my laptop with an UDOO x86 maker board. I haven't finish it.  
OK, built a laptop, why?? this is my idea, and I willing to do it, just it.  
I want to build a laptop belong to me. A hackable laptop, maybe with some other functions.  
Due to the performance of the board, I didn't pay much expect on the performace.  
I just want to coding and interneting, etc. not to run a simulation.  
Anyway I think this board will meet what I need.  

I did some search on DIY laptop about some people done before.  
Many hackers built laptop based on Raspberry pi, with screen keyboard, battery, etc.  
I think these laptop maybe hard to use in reality.  
I want to get a [Bunnie's](http://hackaday.com/2014/04/02/bunnie-launches-the-novena-open-laptop/) opensoure laptop, but it's expensive for me.  
After I saw the UDOO x86 board, I only have one idea that is built one.  

In my previous article I received my UDOO board with 32G emmc.  
And I installed Ubuntu and tested the wifi card, all of them wordk fine.  
In my idea, I will use the exited laptop case(like Thinkpad T450, you can find in aliexpress or ebay).  
This is my finished case and I did a test with raspberry Pi which I used to watch movies on [Kodi](http://wdyggh.github.io/embedded/aria2_RPi.html).  
The only thing I pay a lot of attention is the thickness.  
Due to the PCI-E slot, the board approach to 2.2cm.  
![udoo_x86_2_1.jpg](http://7xifyp.com1.z0.glb.clouddn.com/udoo_x86_2_1.jpg){: .max-height-image}  


Until now, I prepared something that need:  
* motherboard - UDOO x86 Advanced Plus (32G EMMC)
# add pic
* frame - full Thinkpad T450 case(cover)
* screen - 14' inch lcd with eDP interface
* video interface - HDMI to eDP interface board(has a frameware to control brightness.. ) and flex(FPC) HDMI cable
* storage - 60G SSD and SATA cable, Power cable
* power - 12v 3A power adapter
* keyboard - 1.Rii wireless keyboard with touchpad 2.T450 keyboard

Something to prepare:  
* battery and charger with power selector circuit 

Before I received the UDOO board, I tesed the frame, lcd, interface board, and all of them work well.  

Here I want to talk about the video interface board, as we know as the UDOO board has 2 MINI DP++, and my Lcd has the eDP interfece. Earily I search the relationship between the MINI DP++ and eDP, I know they has the same 4wire data wire, but the MINI DP++ has no function to control the brightness of LCD. If I can used the interface of MINI DP++, I need to add a device to control the brightness. The big problem is I can't find some example about how to change MINI DP++ to eDP, except a cable can connect the MINI DP++ and eDP all of them. So, I give up to use the MINI DP++ as the lcd source.  
**UPDATE 1710525** I saw use the dp to edp exmaple on the 51nb bbs. I will check it later.  

Recently, I finished the test on the video output to the lcd.   
In the last blog, becasuse of the bad SATA power cable, I can't use the SSD yet.  
I ordered the JST 4Pin cable for the power connector and 2 Pin cable for the speaker connector on the board.  
I will finished the power cable DIY as soon as received the package.  
Next I will do is the most challenging thing, put the board in the case.  




If you have idea, please leave the comment.

![](){: .center-image}
![](){: .max-height-image}


#### *Reference:*  

1. []()  
2. []()  


- - - 

### [TOP](#top)
