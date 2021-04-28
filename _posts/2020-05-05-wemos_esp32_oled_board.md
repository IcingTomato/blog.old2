---
layout: post
title: "Let's light Up the WEMOS-ESP32 OLED"
description: "WEMOS-ESP32 OLED Tutorial"
comments: false
keywords: "WEMOS-ESP32 OLED, ESP32"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=27733963&auto=1&height=66"></iframe>

# 前言

这个我在淘宝上买的，逛了好久定下买这个

[esp32 OLED OLED模块esp32 for WiFi和蓝牙 ESP ESP32](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.2e212e8dRU7rg5&id=554493925832&_u=934dgkcf688a)

![](//panzhifei.fun/img/2020/05/05/02/p1.jpg)

# 准备

- [Arduino IDE](https://www.arduino.cc/en/Main/Software)
- CP210x [Windows](https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/drivers/CP210x_VCP_Windows.zip)  [macOS](https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/drivers/CP210x_VCP_MacOS.zip)

下面以Windows7 为例进行调试

## 安装Arduino IDE

浏览器打开 [Arduino 官网](https://www.arduino.cc/en/Main/Software)

选择安装包

![](//panzhifei.fun/img/2020/05/05/02/p2.jpg)

![](//panzhifei.fun/img/2020/05/05/02/p3.jpg)

双击下载好的 IDE 可执行文件，全过程保持默认的选择，包括安装路径也是默认。

![](//panzhifei.fun/img/2020/05/05/02/p4.jpg)

## 安装串口驱动CP210x

![](//panzhifei.fun/img/2020/05/05/02/p5.jpg)

双击运行

![](//panzhifei.fun/img/2020/05/05/02/p6.jpg)

![](//panzhifei.fun/img/2020/05/05/02/p7.jpg)

> 检查确认 COM 串口号，以确定串口驱动是否安装成功：

将 Core 通过 USB Type-C 线连接电脑，打开 Windows 设备管理器，点击 端口 (COM 和 LPT) 以查看串口号。然后拔掉 USB 线，此时端口 (COM 和 LPT) 上消失的 COM 口就是该 Core 对应的 串口号。

![](//panzhifei.fun/img/2020/05/05/02/p8.jpg)

## 安装ESP32的板管理

打开IDE，选择 文件 → 首选项 → 设置

![](//panzhifei.fun/img/2020/05/05/02/p9.jpg)

![](//panzhifei.fun/img/2020/05/05/02/p11.jpg)

复制下面的 ESP32 板管理网址到 【附加开发板管理器:】 中

```shell
https://dl.espressif.com/dl/package_esp32_index.json
```

![](//panzhifei.fun/img/2020/05/05/02/p12.jpg)

选择 工具 → 开发板: → 开发板管理器...

![](//panzhifei.fun/img/2020/05/05/02/p13.jpg)

在新弹出的对话框中，输入并搜索 ESP32，点击安装

![](//panzhifei.fun/img/2020/05/05/02/p14.jpg)

在 工具 → 开发板： → 中选择 WEMOS LOLIN 32

![](//panzhifei.fun/img/2020/05/05/02/p15.jpg)

![](//panzhifei.fun/img/2020/05/05/02/p16.jpg)

到此，环境初步搭建完成

# 开始

在IDE中安装库，或者在github上下载zip库安装

项目 → 加载库 → 添加一个zip库

![](//panzhifei.fun/img/2020/05/05/02/p17.jpg)

上Github找就行了，我不多赘述

现在打开一个demo

![](//panzhifei.fun/img/2020/05/05/02/p18.jpg)

文件 → 示例 → ESP8266 and ESP32 Oled Driver for SSD1306 display

下面随便一个demo

我用了时间demo

要修改一下

鉴于此开发板用的是SS1306 的I2C 的OLED

注意：

- SDA → Pin 5 （DATA）
- SCL → Pin 4 （CLOCK）

所以demo里面

第65行

![](//panzhifei.fun/img/2020/05/05/02/p22.jpg)

```
SSD1306Wire  display(0x3c, D3, D5);
```

改成

```
SSD1306Wire  display(0x3c, 5, 4);
```

不然屏幕不亮不要怪老板

然后编译上传

> 注意
> 
> 这个板子有点坑爹，硬件上有个bug
>
> 在上传程序的时候，如果你把板子放在一边不管它，那就会出现

![](//panzhifei.fun/img/2020/05/05/02/p19.jpg)

只要在出现Connecting........ 的时候

按住Boot键

![](//panzhifei.fun/img/2020/05/05/02/p20.jpg)

![](//panzhifei.fun/img/2020/05/05/02/p21.jpg)

成功入门

# 后记

记得记得一定要记得先搞清楚引脚定义再进行开发

网上找的代码先要读懂再编译上传

线不能乱接，搞不好电脑的南桥不保

# 常用库

![](//panzhifei.fun/img/2020/05/05/03/x1.jpg)

这些是我用过的常用库，按需下载

# 视频

[WEMOS ESP32 播放 Bad Apple 60帧](https://www.bilibili.com/video/av95191073)

<iframe height=400 width=600 src="//player.bilibili.com/player.html?aid=95191073&bvid=BV1XE411N7vQ&cid=162975887&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

[迷你ESP32-OLED显示粉丝牌](https://www.bilibili.com/video/BV1H7411d7k6)

<iframe height=400 width=600 src="//player.bilibili.com/player.html?aid=97006654&bvid=BV1H7411d7k6&cid=165601756&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>