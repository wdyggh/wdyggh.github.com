---
layout: post
category: "embedded"
title: "[E]raspicam_tracking with opencv"
tags: ["raspberrypi","opencv","raspcam"]
---



<a name="top"></a>
##  raspicam_tracking with opencv

- - - 

* #### step1: install your raspcam on raspberry pi like this and enter the `raspi-config` enable cam
  > <img src="/images/raspcam_track/1.jpg" alt="替代文本" title="1.jpg" width="700" />  
  > <img src="/images/raspcam_track/2.jpg" alt="替代文本" title="2.jpg" width="700" />    
  
* #### step2: compilation  
    1. get source code [`here`](https://github.com/raspberrypi/userland)
    2. unzip the file and copy the directory under /opt/vc
    3. go to opt/vc and type : sed -i ‘s/if (DEFINED CMAKE_TOOLCHAIN_FILE)/if (NOT DEFINED CMAKE_TOOLCHAIN_FILE)/g’ makefiles/cmake/arm-linux.cmake
    4. create a build directory and compile (it takes a while)   

        ```cpp
        string &operator+(const string& A,const string& B) //cpp TEST
        ```   
        ```bash
        sudo mkdir build
        cd build
        sudo cmake -DCMAKE_BUILD_TYPE=Release ..
        sudo make
        sudo make install
        ```  
    5. Binary should be under /opt/vc/bin   
    Go to /opt/vc/bin and test one file typing : ./raspistill -t 3000   

* #### step3: creat a project
   1.  here is my [source code](http://yunpan.cn/cKGtGmFVtSN7V  ) passwd `069e`  
   2. remove then content of CMakeLists.txt and replace with :  
            `project( YOUR CODE NAME )
            find_package( OpenCV REQUIRED )
            include_directories(/opt/vc/userland/host_applications/linux/libs/bcm_host/include)
            include_directories(/opt/vc/userland/host_applications/linux/apps/raspicam/gl_scenes)
            include_directories(/opt/vc/userland/interface/vcos)
            include_directories(/opt/vc/userland)
            include_directories(/opt/vc/userland/interface/vcos/pthreads)
            include_directories(/opt/vc/userland/interface/vmcs_host/linux)
            include_directories(/opt/vc/userland/interface/khronos/include)
            include_directories(/opt/vc/userland/interface/khronos/common)
            include_directories(./gl_scenes)
            include_directories(.)
            include_directories(/opt/vc/include)
            include_directories(/opt/vc/include/interface/vcos)
            include_directories(/opt/vc/include/interface/vcos/pthreads)
            include_directories(/opt/vc/include/interface/vmcs_host/linux)
            add_executable( YOUR CODE NAME `YOUR CODE NAME.cpp` RaspiCamControl.c RaspiCLI.c RaspiPreview.c RaspiTex.c RaspiTexUtil.c gl_scenes/teapot.c gl_scenes/models.c gl_scenes/square.c gl_scenes/mirror.c gl_scenes/yuv.c gl_scenes/sobel.c tga.c)
            target_link_libraries( `YOUR CODE NAME` /opt/vc/lib/libmmal_core.so /opt/vc/lib/libmmal_util.so /opt/vc/lib/libmmal_vc_client.so /opt/vc/lib/libvcos.so /opt/vc/lib/libbcm_host.so /opt/vc/lib/libGLESv2.so /opt/vc/lib/libEGL.so pthread ${OpenCV_LIBS} )`
   3. compile  
      ```bash
      cmake .   
      make    
      ./YOUR CODE NAME   
      ```
   4. adjust HSV value  
  > <img src="/images/raspcam_track/4.jpg" alt="替代文本" title="4.jpg" width=auto />    
   5. it track only one color and one things  
  > <img src="/images/raspcam_track/6.jpg" alt="替代文本" title="6.jpg" width=auto />    


- - - 

###[TOP](#top)
