---
layout: post
category: "IDE"
title: "Ubuntu下安装配置Sublime Text3"
tags: [“Ubuntu”,"IDE"]
---

<a name="top"></a>

### Sublime Text3

`Sublime Text3` 就不多介绍了  
开门见山  

* 1. 安装方法
通过ppa安装，打开终端，输入以下命令：

```bash
sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-get update
sudo apt-get install sublime-text-installer
```

卸载命令：

```bash
sudo apt-get remove sublime-text-installer
```

* 2. 安装 Package Control 
打开 `sublime text` 按"ctrl+`"访问,输入以下代码

```python
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by) 
```

以上代码会自动创建Installed Packages文件夹，然后使用http下载`Package Control.sublime-package` 等待Package Control安装完成。之后使用`Ctrl + Shift + P`打开命令板，输入PC应出现Package Control等下拉条

* 3 插件安装  
成功安装Package Control 后,就能安装中文编码支持,按`ctrl+shift+p`打开命令板输入`pci`选择`package control install package`,在新的面板里输入`ConvertToUTF8`安装一下插件就可以识别了。该插件支持简体中文，繁体中文，日文，韩文等(GB2312,GBK,BIG5,EUC-KR,EUC-JP)

    插件推荐:   
    * `Markdown preview` Markdown预览插件
    * `SublimeLinter` 语法高亮插件

* 4 个性化配置  
sublime的默认配置文件在`Preferences->Settings-Default`  
我们需要的是在sublime的默认配置文件在Preferences->Settings-User中添加  
比如: 要显示所有空格  
在Default中找到`"draw_white_space": "selection",`  
在User中添加`"draw_white_space": "all",` all代表显示所有  

```json
{
    "color_scheme": "Packages/User/SublimeLinter/Monokai (SL).tmTheme",  //主题
    "draw_white_space": "all",   //显示空格
    "font_size": 9,    //字体大小
    "word_wrap": "true", //自动换行
    "ignored_packages":  //忽略的插件
    [
        "Vintage"
    ]
}
```

* 5 非主题 安装搜狗输入法  
在[官网](http://pinyin.sogou.com/linux/?r=pinyin)下载对应的安装包  
双击 deb安装包,直接安装搜狗输入法.重启即可  

* 6 输入中文  
    * 1 保存以下代码 存为`sublime-imfix.c`文件  

        ```c  
        /*
        sublime-imfix.c
        Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
        By Cjacker Huang
         
        gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
        LD_PRELOAD=./libsublime-imfix.so subl
        */

        #include <gtk/gtk.h>
        #include <gdk/gdkx.h>
        typedef GdkSegment GdkRegionBox;
         
        struct _GdkRegion
        {
          long size;
          long numRects;
          GdkRegionBox *rects;
          GdkRegionBox extents;
        };
         
        GtkIMContext *local_context;
         
        void
        gdk_region_get_clipbox (const GdkRegion *region,
                    GdkRectangle    *rectangle)
        {
          g_return_if_fail (region != NULL);
          g_return_if_fail (rectangle != NULL);
         
          rectangle->x = region->extents.x1;
          rectangle->y = region->extents.y1;
          rectangle->width = region->extents.x2 - region->extents.x1;
          rectangle->height = region->extents.y2 - region->extents.y1;
          GdkRectangle rect;
          rect.x = rectangle->x;
          rect.y = rectangle->y;
          rect.width = 0;
          rect.height = rectangle->height;
          //The caret width is 2;
          //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
          if(rectangle->width == 2 && GTK_IS_IM_CONTEXT(local_context)) {
                gtk_im_context_set_cursor_location(local_context, rectangle);
          }
        }
         
        //this is needed, for example, if you input something in file dialog and return back the edit area
        //context will lost, so here we set it again.
         
        static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
        {
            XEvent *xev = (XEvent *)xevent;
            if(xev->type == KeyRelease && GTK_IS_IM_CONTEXT(im_context)) {
               GdkWindow * win = g_object_get_data(G_OBJECT(im_context),"window");
               if(GDK_IS_WINDOW(win))
                 gtk_im_context_set_client_window(im_context, win);
            }
            return GDK_FILTER_CONTINUE;
        }
         
        void gtk_im_context_set_client_window (GtkIMContext *context,
                  GdkWindow    *window)
        {
          GtkIMContextClass *klass;
          g_return_if_fail (GTK_IS_IM_CONTEXT (context));
          klass = GTK_IM_CONTEXT_GET_CLASS (context);
          if (klass->set_client_window)
            klass->set_client_window (context, window);
         
          if(!GDK_IS_WINDOW (window))
            return;
          g_object_set_data(G_OBJECT(context),"window",window);
          int width = gdk_window_get_width(window);
          int height = gdk_window_get_height(window);
          if(width != 0 && height !=0) {
            gtk_im_context_focus_in(context);
            local_context = context;
          }
          gdk_window_add_filter (window, event_filter, context);
        }
        ```

    * 2 安装C/C++编译环境和GTK libgtk2.0

    ```bash
    sudo apt-get install build-essential
    sudo apt-get install libgtk2.0-dev
    ```

    * 3 编译共享内库

    ```bash
    gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
    ```

    * 4 设置 `LD_PRELOAD` 并启动 Sublime Text

    ``` bash
    LD_PRELOAD=./libsublime-imfix.so subl
    ```

    * 5 打开终端 `sudo gedit /usr/share/applications/sublime-text.desktop`修改`Exec`  


    ``` c  

    [Desktop Entry]
    [...]
    Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text %F
    [...]
     
    [Desktop Action Window]
    [...]
    Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text -n
    [...]
     
    [Desktop Action Document]
    [...]
    Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text --command new_file
    [...]

    ```

    * 6 把 `libsublime-imfix.so` 放到 `/opt/sublime_text/` 中

    ```bash
    mv libsublime-imfix.so /opt/sublime_text/
    ```

    * 7 修改 /usr/bin/subl 
    打开/usr/bin/subl 
    
    ```bash
    sudo gedit /usr/bin/subl
    ```

    修改为

    ```bash
    #!/bin/sh
    export LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so
    exec /opt/sublime_text/sublime_text "$@"
    ```

    * 8 以图为证
    ![ubuntu_sublime_text3](http://7xifyp.com1.z0.glb.clouddn.com/ubuntu_sublime_text3.png)



- - - 

### [TOP](#top)
