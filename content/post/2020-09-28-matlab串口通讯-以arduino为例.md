---
title: MATLAB串口通讯——以Arduino为例
author: WHL
date: '2020-09-28'
slug: matlab串口通讯-以arduino为例
categories:
  - 个人
tags:
  - 单片机
comments: no
images: ~
---

Arduino代码

每10s发送一次"Hello World!"给上位机，当收到上位机的任意字符串string，返回received string。

```{c}
String inputString = "recieved ";
bool stringComplete = false;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(9600);
  inputString.reserve(200);
}

void loop() {
  analogWrite(LED_BUILTIN, 150);
  delay(10000);
  Serial.println("Hello World!");
  if (stringComplete) {
    Serial.println(inputString);
    inputString = "recieved ";
    stringComplete = false;
  }
}

void serialEvent() {
  while (Serial.available()) {
    char inChar = (char)Serial.read();
    inputString += inChar;
    if (inChar == '\n') {
      stringComplete = true;
    }
  }
}
```

MATLAB代码

1. 普通串口通讯
```{matlab}
s=serial('com3');
set(s,'BaudRate',9600);  %设置波特率s

%打开串口
fopen(s);

%写入串口
str = ('hello world');
fprintf(s, str ,'async');
% 读取串口
fgetl(s)

%关闭串口
fclose(s);
```

2.以事件的方式使用串口
```{matlab}
global s

s=serial('com3');%创建串口
set(s,'BaudRate',9600); %设置波特率
set(s,'inputBufferSize',1024000) %设置输入缓冲区域为1M
%串口事件回调设置
set(s,'BytesAvailableFcnMode','terminator');%设置中断响应函数对象
set(s,'Terminator','CR');%设置终端触发方式
s.BytesAvailableFcn=@ReceiveCallback;%ReceiveCallback是中断的触发函数，这里我是定义的。系统的回调函数为instrcallback;
fopen(s);%打开串口

% fclose(s);
%clear s;
```

```{matlab}
% 回调函数
function ReceiveCallback(obj,event)%创建中断响应函数  
    global s
    str = fgetl(s)
end
```

真心感觉MATLAB前途无量！工科的不会用MATLAB，跟废物没什么区别。如果只会写一些简单的m文件，那也水平一般，要会用simulink、app designer、神经网络工具箱、优化工具箱用起来，真的好用，并且能解决问题！