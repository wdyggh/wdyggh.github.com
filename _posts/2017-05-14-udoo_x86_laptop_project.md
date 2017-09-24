---
layout: post
category: "UDOO_X86"
title: "UDOO x86 laptop project"
tags: ["laptop","udoo_x86"]
---

### A project based on UDOO x86 board  
{: #top}

Hello everyone!  
This an process about how I built my laptop with an UDOO x86 maker board. I haven't finish it. OK, built a laptop, why?? this is my idea, and I willing to do it, just it. I want to build a laptop belong to me. A hackable laptop, maybe with some other functions. Due to the performance of the board, I didn't pay much expect on the performace. I just want to coding and interneting, etc. not to run a simulation. Anyway I think this board will meet what I need.  

I did some search on DIY laptop about some people done before. 
Many hackers built laptop based on Raspberry pi, with screen keyboard, battery, etc. I think these laptop maybe hard to use in reality. I want to get a [Bunnie's](http://hackaday.com/2014/04/02/bunnie-launches-the-novena-open-laptop/) opensoure laptop, but it's expensive for me. After I saw the UDOO x86 board, I only have one idea that is built one.  

In my previous article I received my UDOO board with 32G emmc. 
And I installed Ubuntu and tested the wifi card, all of them wordk fine. In my idea, I will use the exited laptop case(like Thinkpad T450, you can find in aliexpress or ebay). This is my finished case and I did a test with raspberry Pi which I used to watch movies on [Kodi](http://wdyggh.github.io/embedded/aria2_RPi.html). I tesed the frame, lcd, interface board, and all of them work well. The only thing I pay a lot of attention is the thickness. Due to the PCI-E slot, the board approach to 2.2cm.  
![udoo_x86_2_1.jpg](http://7xifyp.com1.z0.glb.clouddn.com/udoo_x86_2_1.jpg){: .max-height-image}  


Until now, I prepared something that need:  
* motherboard - UDOO x86 Advanced Plus (32G EMMC)
* frame - full Thinkpad T450 case(cover) [^1]
* screen - 14' inch lcd [^2] with eDP interface  
* video interface - HDMI to eDP interface board [^3] (with a frameware to control brightness.. ) and flex(FPC) HDMI cable [^4]
* storage - 60G SSD and SATA cable, Power cable [^5]
* power - 12v 3A power adapter
* keyboard - 1.Rii wireless keyboard with touchpad [^6] 2.T450 keyboard

Something to prepare:  
* battery and charger with power selector circuit 

Here I want to talk about the video interface board, as we know as the UDOO board has 2 MINI DP++, and my Lcd has the eDP interfece. Earily I search the relationship between the MINI DP++ and eDP, I know they has the same 4wire data wire, but the MINI DP++ on board has no function to control the brightness of LCD. If I can used the interface of MINI DP++, I need to add a device to control the brightness. The big problem is I can't find some example about how to change MINI DP++ to eDP, except a cable can connect the MINI DP++ and eDP all of them. So, I give up to use the MINI DP++ as the lcd source.  

**UPDATE 1710525**  
I saw use the dp to edp exmaple on the 51nb bbs. I will check it later. Recently, I finished the test on the video output to the lcd.  
In the last blog, becasuse of the bad SATA power cable, I can't use the SSD yet. I ordered the JST 4Pin cable for the power connector and 2 Pin cable for the speaker connector on the board. I will finished the power cable DIY as soon as received the package. Next I will do is the most challenging thing, put the board in the case.  

**UPDATE 170611**  
I received JST cable [^5] both 4pin for SATA power and 2pin for speaker connector. After solding wire with power connectors [^7], including SSD driver all of them work fine.  
Next, I will plan how to deal with laptop case. I have print the same size of board on A4 page already. I'm looking for another wireless keyboard with a larger and good performance touchpad [^8].  

**UPDATE 170924**  
I'm a lazy man, this update is after 3 months. During the almost 4 months, I just did a little things.  
![udoo_x86_2_2](http://7xifyp.com1.z0.glb.clouddn.com/udoo_x86_2_2.jpg){: .max-height-image}  
Due to the thickness of laptop cover, the RJ45 socket was removed by a 10 pin adapter cable, then the adapter cable will connect to a RJ45 board [^9] on the laptop's RJ45 position. And the SATA data socket also was extended by a 20cm cable. After these changes, I connected my 60G SATA SSD, the board operates good.  
![udoo_x86_2_3](http://7xifyp.com1.z0.glb.clouddn.com/udoo_x86_2_3.jpg){: .max-height-image}  
![udoo_x86_2_4](http://7xifyp.com1.z0.glb.clouddn.com/udoo_x86_2_4.jpg){: .max-height-image}  

On the other hand, I deal with the T450 C,D case, remove some parts which is block the board. And drill a square that the higest PICE socket can through it to close the C,D case. But, after what I think the limit I did, I get a conclusion, the case is very difficult to close. So, I change my mind, I will design a 3D printed D case to fit the UDOO x86 board, which can has a comfortable space to fix and conveient to extend the IO port(HDMI, USB, DP++, power, etc.). Actually, this blog [3d-printed-laptop-case](https://all3dp.com/3d-printed-laptop-case/) gives me some inspiration. I will design the bone of the D case, to make sure the lowest height needed in this situaion. This is the first step I will go.  
Recently, I saw a lot of people viewed this article, I will do this project as fast as I can.

*If you have something to say, please leave the comment.*  


#### *Reference:*  

1. [3d-printed-laptop-case](https://all3dp.com/3d-printed-laptop-case/)  
2. []()  

[^1]: [aliexpress-T450 cover](https://www.aliexpress.com/wholesale?SearchText=T450+cover&opensearch=true)  
[^2]: LP140WH8(TP)(D2)  
[^3]: [aliexpress-edp board](https://www.aliexpress.com/wholesale?SearchText=edp+board&opensearch=true)
[^4]: [aliexpress-flex HDMI cable](https://www.aliexpress.com/wholesale?SearchText=flex+hdmi+cable&opensearch=true)
[^5]: JST 2.0mm 4pin
[^6]: Rii RT-MWK12+ US_layout
[^7]: [wiki-Serial_ATA_Power_connectors](https://en.wikipedia.org/wiki/Serial_ATA#Power_connectors)
[^8]: [aliexpress-Rii keyboard](https://www.aliexpress.com/item/Genuine-New-Rii-K18-Large-Size-2-4GHz-Wireless-Multimedia-Mini-Keyboard-Touchpad-Air-Mouse-For/32760251941.html?spm=2114.01020208.3.134.TYPsbH&s=p&ws_ab_test=searchweb0_0,searchweb201602_2_10152_10065_10151_10068_10084_10083_10080_10082_10081_10110_10136_10137_10157_10175_10111_10060_10138_10112_10113_10155_10062_10114_10156_10154_10056_10181_10055_10054_10182_10059_10099_10078_10079_10103_10073_10102_10096_10070_10123_10052_10053_10142_10107_10050_10051,searchweb201603_4,ppcSwitch_3_ppcChannel&btsid=5ed271fd-01bc-4111-853d-60fe9fd55420)
[^9]: [aliexpress rj45+board](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20170924005751&SearchText=rj45+board)

- - - 

### [TOP](#top)

#### *Footnote:*