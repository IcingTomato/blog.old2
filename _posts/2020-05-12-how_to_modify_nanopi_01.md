---
layout: post
title: "Let's play FriendlyARM NanoPi-Episode 1"
description: "How to use Linux"
comments: false
keywords: "Linux, NanoPi, FriendlyARM"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=27733963&auto=1&height=66"></iframe>

# 前言

一咬牙，买了这个NanoPi

（花呗12期预定）

FriendlyARM NanoPi Neo2 Black + NanoHatOLED

详细配置请见NanoPi NEO2 Black Wiki [中文](//wiki.friendlyarm.com/wiki/index.php/NanoPi_NEO2_Black/zh#.E6.89.8B.E5.86.8C.E5.8E.9F.E7.90.86.E5.9B.BE.E7.AD.89.E5.BC.80.E5.8F.91.E8.B5.84.E6.96.99) / [Engish](//wiki.friendlyarm.com/wiki/index.php/NanoPi_NEO2_Black)

# 魔改 NanoHatOLED

众 所 周 知

OLED容易烧屏

特别是长时间在同一个区域显示同一片文字

![](//panzhifei.fun/img/2020/05/12/01/01.jpg)

- 图片源自 [稚晖君-【硬核】真●自制超迷你个人服务器 树莓派你可以退群了？](https://www.bilibili.com/video/BV1q7411h73t)

<iframe height=400 width=600 src="//player.bilibili.com/player.html?aid=87134130&bvid=BV1q7411h73t&cid=148884865&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

所以魔改了原来的[BakeBit](https://github.com/friendlyarm/BakeBit)

这是[我魔改过的](https://github.com/Peter-Zhifei/BakeBit)

详细使用在下面有README

# Ubuntu 使用的基础配置

## 更换 Ubuntu-Ports 镜像源和Python pip源（一）

```shell
$ wget //112.124.9.243/aptsouce.sh
$ chmod 755 aptsouce.sh
$ sudo -H ./aptsouce.sh
$ sudo apt-get update
```

或者

```shell
$ git clone https://github.com/ch1y4/NanoPi.git
$ cd NanoPi
$ chmod 755 aptsouce.sh
$ sudo -H ./aptsouce.sh
$ sudo apt-get update
```

## 更换 Ubuntu-Ports 镜像源（二）

```shell
#备份sources.list
$ cp /etc/apt/sources.list /etc/apt/sourses.list.backup
#换清华源
#把 ports.ubuntu.com 替换成 mirrors.tuna.tsinghua.edu.cn/ubuntu-ports
#按 Ctrl+\ 进行全局替换
$ sudo nano /etc/apt/sources.list
#保存并更新
$ sudo apt-get update
$ sudo apt-get upgrade
```

## NTP 自动对时

```shell
$ sudo apt-get install ntp
$ sudo nano /etc/ntp.conf
#在/etc/ntp.conf 文件最后面添加 
server ntp.ntsc.ac.cn
```

## 设置时区

```shell
#查看当前时区
$ date -R
#修改时区
$ tzselect
#复制文件到/etc目录下
$ cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
#再次查看当前时间
$ date -R
```

## 命令行挂载Samba服务器

```shell
#下载samba相应组件
$ sudo apt-get install cifs-utils
#查看共享目录
$ smbclient -L IP地址 -N
#挂载(username=服务器的名字，密码=服务器密码，IP地址＝自己服务器的IP)
$ sudo mount -t cifs -o username=用户名,password=密码 //IP地址/目录 /本地挂载目录
#解除挂载
$ sudo umount /挂载的目录
```

## Ubuntu 安装 Neofetch/Screenfetch(个性化显示 Linux 系统信息)

```shell
$ sudo apt-get install python-software-properties software-properties-common
$ sudo add-apt-repository ppa:dawidd0811/neofetch
$ sudo apt-get update
$ sudo apt-get install neofetch screenfetch
```

# 附加一点

千万千万不要用

```shell
$ sudo apt-get autoremove
```

直接干掉没用的和有用的依赖

```shell
$ sudo apt-get dist-upgrade
```

用这个专治

```shell
0 upgraded, 0 newly installed, 0 to remove and 6 not upgraded
```

# 推荐几个NanoPi的博客

- [NoColor's Blog](https://www.nocolor.pw/)

- [ccbirds blog](//ccbirds.cn/)

- [ChiKoiDAC(要手段)](https://sites.google.com/view/chikoidac/home)
