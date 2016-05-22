---
layout: post
category: "blackberry"
title: "BB10 DEV IDE setting on Ubuntu 15.04"
tags: ["BB10"]
---


### BB10 Getting Statred

<a name="top"></a>
##Native SDK for BB10##

##1 Download Momentics IDE for Blackberry  ##
Go to [HomePage](https://developer.blackberry.com/native/download/) and download the `momentics IDE`,but after the downloading finishded,i don't know how to install the `IDE`. So, i back to the home page and search for the methods.   
Then, i find this [page](https://developer.blackberry.com/native/downloads/requirements/). It's shows the system Requirments.You will see the command line like below:   

```bash
//To run the Momentics IDE on Ubuntu 14.04 (32-bit and 64-bit), you need to install the following library:

sudo apt-get install libwebkitgtk-1.0

//To run the Momentics IDE on Ubuntu 14.04 (64-bit), you need to install the following additional libraries:

sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0
sudo apt-get install lib32stdc++6
sudo apt-get install libgtk2.0-0:i386 libxtst6:i386
```

But the `lib32bz2-1.0`lib cann't be installed.  
and use `apt-cache search lib32bz2-1.0`serach the package ,nothing was show.  
Back to `Momentics IDE` I click the `.run`file but nothing happened.Next I find the [youtube](https://www.youtube.com/watch?v=1NTCBCjM6vY), shows how to install this IDE on linux.

> in the file directory open terminal 
> `chmod +x`
> `./filename`
> press `q`to continue

**If finished** the current directory will find a new folder `bbndk`  
go to the `bbndk` by the terminal, and try `./qde`  

and then it will show like this   
![bb10_require_device_connect.png](http://7xifyp.com1.z0.glb.clouddn.com/bb10_require_device_connect.png)   
  
needed to connect a BB10 device  

**so i searched google & [Blackberry Support Forums](https://supportforums.blackberry.com/t5/Application-Platforms/ct-p/app_plat)tried so many methods**eventaully i found how to connect to My Passport via wifi.  
so here is the method how to connect to `Momentics IDE` via `wifi`   
> **on bb10 device** go to `setting`>`storage&sharing`>turn on`develop mode` > remember the `IP`  

> go to blackberry develop site and get the `bbidtoken.csk`, then i put it into ~/.rim  

> on `Momentics IDE` in the `Project Explorer`  pane on the left, Right click, choose `NEW > BlackBerry Target`, in the `connection` group box enter the IPV4 IP address  

> back to the `Project Explorer` right click your target > Blackberry Tools > connect.  


if connected it wii show like below:  
![momenticside_device_connected.png](http://7xifyp.com1.z0.glb.clouddn.com/momenticside_device_connected.png)


so next i wiil follow the [Guide](https://developer.blackberry.com/native/documentation/getting_started/first_app/index.html) or open in Momentics IDE   
![help_contents.png](http://7xifyp.com1.z0.glb.clouddn.com/help_contents.png)

Have a good luck.



### How to get ID token

Here is [ID token](https://www.blackberry.com/SignedKeys/codesigning.html)

![blackberryIDToken1.png](http://7xifyp.com1.z0.glb.clouddn.com/blackberryIDToken1.png)

![blackberryIDToken2.png](http://7xifyp.com1.z0.glb.clouddn.com/blackberryIDToken2.png)

![blackberryIDToken3.png](http://7xifyp.com1.z0.glb.clouddn.com/blackberryIDToken3.png)

### How to get debug token

Go to `Window`>`Preferences`   
In Preferences window > `Blackberry`>`Signing`   
Here maybe requirst your `Device PINs`&`ID Token`    
That's all

`2015-11-05 updates`

### How to connect device via usb with MomenticsIDE on Ubuntu

when you connect device with computer via usb, it will show a `wired connection`on the internet zone  
Then, edit the `wired connection` like below:  

![usb_connect_to_IDE1.png](http://7xifyp.com1.z0.glb.clouddn.com/usb_connect_to_IDE1.png)  

* connection method : manual  
* address: 169.254.0.2  
* netmask:255.255.255.0  
* gateway: 169.254.0.1  

Last, pair your device in `device manager`
![usb_connect_to_IDE2.png](http://7xifyp.com1.z0.glb.clouddn.com/usb_connect_to_IDE2.png)  



- - - 

###[TOP](#top)
