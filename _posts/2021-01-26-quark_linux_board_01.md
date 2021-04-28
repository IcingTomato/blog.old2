---
layout: post
title: "Let's Play Quark Linux Board - Episode 1: What is Quark?"
description: "Quark Linux Board Simple Tutorial"
comments: false
keywords: "Quark, Linux"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1484844664&auto=1&height=66"></iframe>

# 0x00 简介

<iframe height=400 width=600 src="//player.bilibili.com/player.html?aid=87134130&bvid=BV1q7411h73t&cid=148884865&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

Project-Quantum 量子计划 出自 [哔哩哔哩@稚晖君](https://space.bilibili.com/20259914/)之手

根据稚晖君本人描述其计划分支可以总结位下列的树状图

```shell
Project-Quantum
|
|-- Core
|    |
|    |-- Quark-n
|    |
|    |-- Quark-s
|
|-- Shield
|    |
|    |-- Atom
|
|-- Arduino
|    |
|    |-- Electron
|
|-- Power
|    |
|    |-- Gluno
|
|-- Unit
```

现已在[GitHub@peng-zhihui/Project-Quantum](https://github.com/peng-zhihui/Project-Quantum)开源

[Seeed官方Wiki](https://wiki.seeedstudio.com/cn/Quantum-Mini-Linux-Development-Kit/) 

Seeed官方介绍

> 夸克迷你开发者套件Atom-N可能是市面上最小的Linux卡片电脑, 本套件包含一个搭载四核CPU的高度集成SOM核心板，以及一个多功能IO扩展底板，可以在40mm x 35mm的尺寸上运行Linux系统, 并具备出色的扩展功能。您可以将它用于搭建个人服务器、开发智能语音助手、设计机器人等场景。

![](//panzhifei.fun/img/2021/01/26/01/quark.jpg)

# 0x01 资源特性

+ CPU：Allwinner H3, Quad-core Cortex-A7@1.2GHz
+ GPU：Mali400MP2@600MHz，Supports OpenGL ES2.0
+ DDR3 RAM：512MB
+ 网络：板载RTL8723BU，支持Wi-Fi: IEEE 802.11 b/g/n @2.4GHz和蓝牙: BT V2.1/ BT V3.0/ BT V4.0
+ 麦克风：板载麦克风
+ 存储：板载16GB eMMC
+ 传感器：板载MPU6050运动传感器(陀螺仪 + 加速度计)
+ MicroSD Slot：x1
+ USB &Type-C ：USB 2.0×2 USB Type-C×1（支持供电和数据传输，有OTG功能，注意，早批次的Atom-N插入USB Type-C的两个方向功能时不一样的，一面是USB Serial ，旋转180度后插入则为USB OTG，之后批次的会取消USB-OTG的功能，两面都为USB串口。）
+ 视频输出: 板载240x135TFT显示屏，SPI，IC：ST7789VW
+ 调试串口：集成于USB Type-C，需在电脑上安装CP210x驱动
+ GPIO： 2.0mm间距26针式接头连接器，包括USB OTG，USB串口，I2C，UART，SPI，I2S，GPIO，可多路复用
+ 按键：GPIO-KEY, Uboot, Recovery, Reset
+ PC Size: 31mmx22mm
+ Power Supply: DC 5V/2A
+ 温度工作范围：0摄氏度到80摄氏度
+ OS/Software: U-boot，Ubuntu-Core，OpenWRT（移植中）

![](//panzhifei.fun/img/2021/01/26/01/quarkio.jpg)

# 0x02 接口布局

+ GPIO管脚定义

尚未推算完成

+ Debug Port (UART 0)

尚未推算完成

# 0x03 快速入门

## 准备工作

要开启你的Quark新玩具，请先准备好以下硬件

+ Quark-n主板+Atom扩展板
+ microSD卡/TF卡: Class10或以上的 16GB SDHC卡
+ 一个microUSB接口的外接电源，要求输出为5V/2A（可使用同规格的手机充电器）
+ 一套USB键盘鼠标，同时连接还需要USB HUB （或选购串口转接板，要PC上进行操作）
+ 一台电脑，需要联网

## 经过测试的TF卡

制作启动Quark的TF卡时，建议Class10或以上的 16GB SDHC卡。以下是经本人测试验证过的高速TF卡：

![](//panzhifei.fun/img/2021/01/26/01/sandisk16.jpg)

![](//panzhifei.fun/img/2021/01/26/01/sandisk32.jpg)

![](//panzhifei.fun/img/2021/01/26/01/chuanyu32.jpg)

![](//panzhifei.fun/img/2021/01/26/01/lexar32.jpg)

## 安装系统

### 下载镜像

[Quark-n-21-1-11](https://files.seeedstudio.com/wiki/Quantum-Mini-Linux-Dev-Kit/quark-n-21-1-11.zip)

### 烧写Ubuntu系统

+ 将TF卡插入读卡器，连接电脑，必要时请格式化为FAT32
+ 将 Linux 系统固件和烧写工具 win32diskimager.rar 分别解压，在 Windows 下插入TF卡（限4G及以上的卡)，以管理员身份运行烧写工具 win32diskimager，在烧写工具 win32diskimager 的界面上，选择你的TF卡盘符，选择Linux 系统固件，点击 Write 按钮烧写。

![](//panzhifei.fun/img/2021/01/26/01/win32disk.jpg)

+ 成功烧写后，会看到如下界面：

![](//panzhifei.fun/img/2021/01/26/01/win32disksuccess.jpg)

+ 当制作完成TF卡后，拔出TF卡插入 BOOT 卡槽，上电启动（注意，这里需要5V/2A的供电），你可以看到STAT灯闪烁，这时你已经成功启动系统。

# 0x04 系统使用

## 连接串口

### 下载CP210x驱动

[Silicon CP210x 驱动官网](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

- [Windows](https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/drivers/CP210x_VCP_Windows.zip)  
- [macOS](https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/drivers/CP210x_VCP_MacOS.zip)

选择电脑的操作系统进行下载安装

![](//panzhifei.fun/img/2021/01/26/01/driverchoose.jpg)

如图将USB Type-C线连接夸克和电脑

![](//panzhifei.fun/img/2021/01/26/01/quarkconnect.jpg)

夸克将会自行启动

![](//panzhifei.fun/img/2021/01/26/01/devicesmanager.jpg)

在设备管理器中检查端口（如图为COM16）

打开串口工具（如PuTTY等）

![](//panzhifei.fun/img/2021/01/26/01/putty.jpg)

![](//panzhifei.fun/img/2021/01/26/01/puttywindows.jpg)

## 用户账户

- 默认账户

```shell
用户名: pi
密码: quark
```

- 根用户/超级用户

```shell
用户名: root
密码: quark
```

默认会以 pi 用户自动登录，你可以使用 sudo npi-config 命令取消自动登录。

- 更新软件包：

```shell
$ sudo apt-get update
```

- 更换软件包源和pip源

```shell
$ wget //112.124.9.243/aptsouce.sh
$ chmod 755 aptsouce.sh
$ sudo -H ./aptsouce.sh
$ sudo apt-get update
```

因为原生的中科大源会有些许问题，所以我们将apt换成清华源，pip换成阿里源

## 连接无线局域网

Quark上搭载的Ubuntu 16.04使用NetworkManager来管理网络。

无论是板载 WiFi，USB WiFi还是SD WiFi, 它们的连接方式都是一样的。

经验证的USB WiFI模块

- 小米WiFi mt7601
- 5G USB WiFi RTL8821CU（部分网友反映没有驱动）

目前使用 NetworkManager 工具来管理网络，其在命令行下对应的命令是 nmcli，要连接WiFi，相关的命令如下：

- 切换到root账户

```shell
$ su root
```

- 查看网络设备列表

```shell
$ nmcli dev
```

> 注意，如果列出的设备状态是 unmanaged 的，说明网络设备不受NetworkManager管理，你需要清空 /etc/network/interfaces下的网络设置,然后重启.

- 开启WiFi

```shell
$ nmcli r wifi on
```

- 扫描附近的 WiFi 热点

```shell
$ nmcli dev wifi
```

- 连接到指定的 WiFi 热点

```shell
$ nmcli dev wifi connect "SSID" password "PASSWORD" ifname wlan0
```

> 请将 SSID和 PASSWORD 替换成实际的 WiFi名称和密码。

连接成功后，下次开机，WiFi 也会自动连接。

如果你的USB WiFi无法正常工作, 大概率是因为文件系统里缺少了对应的USB WiFi固件。

可以通过下列命令安装所有的USB WiFi固件:

```shell
$ apt-get install linux-firmware
```

## 使用 npi-config 配置系统

> npi-config是一个命令行下的系统配置工具，可以对系统进行一些初始化的配置，可配置的项目包括：用户密码、系统语言、时区、Hostname、SSH开关、自动登录选项等，在命令行执行以下命令即可进入:

```shell
$ sudo npi-config
```

![](//panzhifei.fun/img/2021/01/26/01/npi.jpg)

### 定制命令行欢迎信息

欢迎信息主要是这个目录下的脚本来打印的：

> /etc/update-motd.d/

比如要修改 FriendlyELEC 的大字LOGO，可以修改/etc/update-motd.d/10-header 这个文件，比如要将LOGO改为Elaina，可将以下行：

> TERM=linux toilet -f standard -F metal $BOARD_VENDOR

改为：

> TERM=linux toilet -f standard -F metal Elaina

### 远程桌面连接

> 系统镜像中包含 `xrdp` 服务 并在正常情况下默认运行，因此您可以使用Windows自带的远程桌面连接软件进入Quark-N的桌面：

- 使用 `ifconfig` 命令获取开发板的ip地址
- 在Windows电脑上搜索 `远程桌面连接` ，打开软件
- ++在同一局域网中，输入开发板的IP地址并登录++
- ~~牛通的伙伴可以将夸克映射到公网上用公网IP来访问~~

![](//panzhifei.fun/img/2021/01/26/01/mstsc1.jpg)

![](//panzhifei.fun/img/2021/01/26/01/mstsc2.jpg)

![](//panzhifei.fun/img/2021/01/26/01/mstsc3.jpg)

![](//panzhifei.fun/img/2021/01/26/01/mstsc4.jpg)



