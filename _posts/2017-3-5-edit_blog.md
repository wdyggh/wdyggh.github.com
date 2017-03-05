---
layout: post
category: "others"
title: "博客完善"
tags: ["jekyll","最近干啥","others"]
---


### 功能完善，内容会继续增加 
{: #top}


从20170101 开始,就一直在完善本博客的功能，  
其中也包括一些新加的，修复的。

* 添加文章访问次数
* 图片css
* 文章后推荐相关阅读
* tag 云
* google analytics
* google search bar

其中大部分都是参考别人博客源码。  

下面就从博客搭建开始说起  
好像有点不太正经哈，之前写了那么多内容怎么现在才开始聊搭建。  

> os: Ubuntu 16.04 LTS

~~~ bash
sudo apt install ruby 
sudo gem update --system 
sudo gem install rubygems-update 
sudo apt-get install ruby-de
sudo gem install jekyll
~~~

具体参考 [jekyll doc](https://jekyllrb.com/docs/installation/)  

git clone 博客到本地  
如果运行 `jekyll serve` 的话可能会报错，  
因为分页插件的问题，没有那是最好  
进入 `_config.yml` 确认 `Gem` 下田间分页插件  

~~~ bash
# Gems
gems: [jekyll-paginate]
~~~

### 添加文章访问次数

接下来说说访问次数：  
具体参考了 [咀嚼之味](http://jerryzou.com/posts/introduction-to-hit-kounter/)  
我也不是计算机专业毕业，  
依葫芦画瓢下来，也没有太大难度  

### 图片css

图片css中之前已经添加过了 `center-image`  
但是没有对图片高度加以限制，  
导致一些太长的图片就充满整页  
修改之处就添加了对高度限制  

~~~ css
.max-height-image
{
    margin: 0 auto;
    display: block;
    width: auto;
    max-height: 400px;
    max-width: 100%;
}
~~~

### 文章后推荐相关阅读

博文结尾推荐‘系统’其实就是按照`tag`来取得相关性的  
本来使用了第三方插件 [jekyll-tagging-related_posts](https://github.com/toshimaru/jekyll-tagging-related_posts),  
按照教程下来，在本地的确好使，  
推送到远程分支后就。。。  
后来问了作者才知道，大多第三方插件，都是不直接被`ghpages`支持的  
使用方法当然有  
是把本地编译好的 `_site` 文件推送到远程分支，  
网上也给出了很多解决办法  
这里我是找到了这个 [github-pages-with-jekyll-custom-plugin](http://gumpcha.github.io/blog/github-pages-with-jekyll-custom-plugin/)  
由于没有经过验证，我也不敢打包票  
文章推荐我是参考了这篇[博客](https://blog.webjeda.com/jekyll-related-posts/)  

### tag 云

添加`tag 云`时参考了好几篇博客  
[咀嚼之味](http://jerryzou.com/all-articles/) [jphome](http://jphome.github.io/tags/#blog-ref) [equation 85](http://equation85.github.io/tags.html#tcl/tk-ref)  
其中咀嚼之味的标签云是经过作者自己重构过了，效果也是出众，  
由于我对js知识欠佳，没能学得来  
具体代码如下：  


![tags cloud1](http://7xifyp.com1.z0.glb.clouddn.com/reedit_blog_tagCloud1.png){: .center-image}

其中博客所有的`tags`，都存在于`site.tags`里  
对tags进行遍历，并取得tag的大小`.size`  
加上css效果就如下：  

![tags cloud](http://7xifyp.com1.z0.glb.clouddn.com/reedit_blog_tagCloud.png){: .center-image}

一下代码接上，为了方便说明就切开了  
接下来就是文章列表了  
按照刚刚的tag顺序，对文章列表遍历  


![tags cloud2](http://7xifyp.com1.z0.glb.clouddn.com/reedit_blog_tagCloud2.png){: .center-image}

### google analytics

之前已经在用 cnzz 作为 分析工具，虽然没什么人来这个站，  
但是看看 至少有个心理作用  
完全由于好奇 添加了 [google analytics](https://www.google.com/intl/zh-CN/analytics/)  
墙内的同学还是cnzz 好用  

### google search bar

最后就是今天刚刚完成的google search bar  
博客之前是使用的第三方的谷歌搜索，  
应该是不能用好久了  
现在改成了原生谷歌，  
参考了 `equation 85` 的源码的源码(因为用了`JB`插件)  
就从[这](https://github.com/equation85/equation85.github.com/blob/master/_includes/themes/the-program/default.html#L31)开始  

- - - - 

最后，我会尽量多写文章，因为器已经利了。  



#### *Reference:*  

1. [jekyll doc](https://jekyllrb.com/docs/installation/)  
2. [咀嚼之味 hit counter](http://jerryzou.com/posts/introduction-to-hit-kounter/)  
3. [jekyll-tagging-related_posts](https://github.com/toshimaru/jekyll-tagging-related_posts)  
4. [github-pages-with-jekyll-custom-plugin](http://gumpcha.github.io/blog/github-pages-with-jekyll-custom-plugin/)  
5. [webjeda](https://blog.webjeda.com/jekyll-related-posts/)
6. [咀嚼之味 tag](http://jerryzou.com/all-articles/)  
7. [jphome tag](http://jphome.github.io/tags/#blog-ref)  
8. [equation 85 tag](http://equation85.github.io/tags.html#tcl/tk-ref)  
9. [google analytics](https://www.google.com/intl/zh-CN/analytics/)
10. [equation 85 search bar](https://github.com/equation85/equation85.github.com/blob/master/_includes/themes/the-program/default.html#L31)  



- - - 

### [TOP](#top)
