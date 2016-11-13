---
layout: post
category: "分类"
title: "matlab中 serial 注意点"
tags: ["serial","matlab"]
---


### matlab中 serial 注意点  

<a name="top"></a>

<code>MATLAB R2015a</code>

Use `<html>` tags for this.  
Here is a literal `` ` `` backtick.
And here is ``  `some`  `` text (note the two spaces so that one is left in the output!).  

This is a ` literal backtick.  
As \`are\` these!  

This is a Ruby code fragment `x = Class.new`{:.language-ruby}  

讨论一下 matlab中打开serial port后 delay给不给的问题，  
具体例子如下：  

~~~matlab
s=serial('COM12','timeout',15);
s.BaudRate=9600;
fopen(s);
pause(1);	%休息1秒
str1=num2str(5);
str1=['a' str1];
pause(1);	%休息1秒
fprintf(s,str1);
tc=fscanf(s,'%s');
fprintf([tc '\n']);
~~~

serial 另一端是arduino，接收到消息后，回发一个数字。  
刚开始写的时候，我也没想到要加一个pause，  
但是执行好几次后都没有收到arduino的回发消息。  
可以确认matlab确实有发送消息，但是arduino端没有反应，  
再推理一下，matlab端没有正确的发送消息。（推理得来。）  
注释其中一个pause，都造成matlab无法接收到回发消息。  
后来试着减少下停顿时间，具体没怎么试，  
(0.1s, 0.5s,..)都没能正确接收，索性留了点余地，给了1s。

在重新整理下，这个问题似乎只存在serial刚打开的时候，  
在之后while中，pause只给了0.1s。也能正确发送接收。  


#### *Reference:*  

1.[无]()  
2.[无]()  

- - - 

### [TOP](#top)
