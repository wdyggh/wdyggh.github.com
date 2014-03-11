---
layout: post
category: "linux"
title:  "Debian/Linux ruby setup"
tags: [linux,Debian,ruby]
---
有别于Windows下的rubyinstall+devkit安装与配置。Debian/Linux下方便多了。

#### 一、安装ruby开发环境
{% highlight bash %}
sudo apt-get install ruby irb rdoc ruby-dev
{% endhighlight %}

#### 二、安装ruby gem
一步就安装好ruby的基本开发环境了。再要安装jekyll什么的就直接：
{% highlight bash %}
sudo gem install rdiscount ruby redcarpet
{% endhighlight %}
