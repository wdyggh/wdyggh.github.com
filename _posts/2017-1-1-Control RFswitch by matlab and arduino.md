---
layout: post
category: "embedded"
title: "Control RFswitch by matlab and arduino"
tags: ["matlab","arduino"]
---


### Control RFswitch by matlab and arduino  

<a name="top"></a>

先来描述一下整个工作流程，主控端是电脑matlab，从机是arduino，再arduino控制开关(SP8T)，RF_SP8T开关有1出入8输出的端口，所以要控制8个输出口，得有3个TTL输入。  
现在的要求是1对23个端口，一般看来至少得有3组sw，但是这3组sw得有3个输入，所以还要再加一个main_sw，作为3个slave_sw的主控。  
控制要求是23个端口中，同一时间内只能开启一个。  
概图如下：  

![rfswitch1](http://7xifyp.com1.z0.glb.clouddn.com/rfswitch1.png){: .center-image }

matlab端作为命令主控要做的就是发送端口号码，通过serial函数。

~~~ matlab
fprintf(com_num,num2str(sw_num));
~~~

arduino端主要有3大部分，  

* 1是接收sw号码
* 2是输出对应pin的值为high，其他为low
* 3是返回给matlab收到的号码。  


~~~ c
/*
  1main 3slave RF_SW  test
  date:20161103
  author:ggh
*/

//A B C To:
// 0 0 0 1
// 1 0 0 2
// 0 1 0 3
// 1 1 0 4
// 0 0 1 5
// 1 0 1 6
// 0 1 1 7
// 1 1 1 8

const int E_A = 2;
const int E_B = 3;
const int E_C = 4;

//char HL[] = {HIGH, LOW};
char sw_Port[][3] = {{0, 0, 0}, {HIGH, LOW, LOW}, {LOW, HIGH, LOW}, {HIGH, HIGH, LOW}, {LOW, LOW, HIGH}, {HIGH, LOW, HIGH}, {LOW, HIGH, HIGH}, {HIGH, HIGH, HIGH}};
const int sw_Pin[][3] = {{2, 3, 4}, {5, 6, 7}, {8, 9, 10}};
const int main_sw_Pin[] = {11, 12, 13};  //5,6,7
int i , j = 0;
int sub_SW_num = 0;
int sub_SW_port = 0;

void write2pin(int sw_Num, int sw_Sta) { //sub_sw,sw_port
  for (i = 0; i < 3; i++) {
    digitalWrite(sw_Pin[sw_Num][i], sw_Port[sw_Sta][i]);
  }
}
void reset_Pin() {
  for (j = 0; j < 3; j++) {
    for (i = 0; i < 3; i++) {
      //      pinMode(sw_Pin[j][i], OUTPUT);
      digitalWrite(sw_Pin[j][i], LOW);
    }
  }
  for (i = 0; i < 3; i++) {
    //    pinMode(main_sw_Pin[i], OUTPUT);
    digitalWrite(main_sw_Pin[i], LOW);
  }
}
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  for (j = 0; j < 3; j++) {
    for (i = 0; i < 3; i++) {
      pinMode(sw_Pin[j][i], OUTPUT);
      digitalWrite(sw_Pin[j][i], LOW);
    }
  }
  for (i = 0; i < 3; i++) {
    pinMode(main_sw_Pin[i], OUTPUT);
    digitalWrite(main_sw_Pin[i], LOW);
  }
}

void loop() {
  char cmd[] = {' ', ' '};
  // put your main code here, to run repeatedly:
  if (Serial.available() > 0) {
    reset_Pin();
    //    cmd = Serial.read();
    //    Serial.readBytes(cmd,2);
    Serial.readBytesUntil('n', cmd, 3);
//    Serial.print(cmd );
    sub_SW_num = (atoi(cmd) - 1) / 8 + 1;   //1,2,3
//    Serial.print(sub_SW_num );
    sub_SW_port = atoi(cmd) - (sub_SW_num - 1) * 8;
    Serial.println(sub_SW_port);          //1~8

    //main sw 5,6,7
    for (i = 0; i < 3; i++) {
      digitalWrite(main_sw_Pin[i], sw_Port[sub_SW_num + 3][i]);
    }
    //sub sw
    write2pin(sub_SW_num - 1, sub_SW_port - 1);

  }
}

~~~

现在测试下来的问题是，loop中cmd为2位，当matlab发送0～9的号码，arduino从收到号码—返回号码的时间大概有1秒左右，当matlab发送2位的号码，arduino从收到号码—返回号码的时间大概只有0.1秒左右。这个问题可能跟cmd的初始化和转换为int有关。  
因为在要求中，整个switching时间却快越好，所有想出了一下解决办法。matlab改为发送hex数字。  

~~~ matlab
dec2hex(num)﻿
~~~

arduino中接收hex再转换成int。  
这一步还是现在的想法，待测试完成后，贴出完整代码。



#### *Reference:*  

1.[hex2int](http://forum.arduino.cc/index.php?topic=311875.0)  
2.[]()  

- - - 

### [TOP](#top)
