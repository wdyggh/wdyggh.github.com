---
layout: post
category: "linux"
title:  "测试2.6内核驱动程序所遇问题解 "
tags: [linux,内核驱动]
---
####一、write ioctl 警告:从不兼容的指针类型初始化
原因在于:write中的char *buf应该为const char *buf；ioctl中的long data为unsigned long data
 
####二、irqreturn函数中的参数变化
2.6中的irqreturn函数中只有两个参数了，原来的irqreturn_t int_interrupt(int irq,void * dev_id,struct pt_regs *regs)；应该是irqreturn_t int_interrupt(int irq,void * dev_id)；
 
####三、2.6内核高版本中的frags值发生变化
原来头文件里没有SA_INTERRUPT了，一般使用IRQF_SHARED 了。  
rquest_irq(PRINT_IRQ,int_interrupt,IRQF_SHARED,INT_DEV_NAME,NULL);
 
####四、中断所需的头文件不同
2.4内核中中断的注册和注销使用的头文件#include <linux/shed.h>  
2.6内核中中断的注册和注销使用的头文件#include <linux/interrupt.h>

####五、预留主设备号和次设备号
1.可用的主设备号范围如下：60~63 120~127 240~254  
2.主设备号10的次设备号中240~255范围也用在测试或特定平台上。
 
####六、printk函数输出
1输出可标记等级，默认为KERN_WARNNING，等同于下面几句：  
printk("<4>" "system ok\n");  
printk("<4> system ok\n");  
printk("system ok\n");  
2.必须使用“\n”字符，否则调试过程混乱。当不使用它时，下一条输出会紧接着前一句，而且会输出标记级别。  
如printk("hello world");printk("goodbye\n");则输出时为hello world<6>goodbye.
 
####七、思考？
1.为什么普通用户在执行./test的时候，总是提示设备文件打开出错，而用root用户执行./test的时候就成功了呢？  
测试解决了，在root用户下将设备文件访问权限改为666，再就可以了。  
2.一个设备文件，不能同时被两个设备同时使用。先打开的成功，后打开的出错。


