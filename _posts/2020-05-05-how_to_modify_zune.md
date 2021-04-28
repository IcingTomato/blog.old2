---
layout: post
title: "Modified My Microsoft Zune"
description: "Nice work, Microsoft Zune."
comments: false
keywords: "Microsoft, Zune"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=27733963&auto=1&height=66"></iframe>

# 前情提要

9102年，我上网淘了两个的Zune，开始了自己的折腾之路。

Zune30，有（张大妈）网友称之为“上古神器”。

我手上的Zune，是第一代，也叫Zune 30。于2006年11月14日发布。

![](//panzhifei.fun/img/2020/05/05/p1.jpg)

这种上古硬盘机，是和iPod Classic有的一拼的。

158.8克，320x240px，133.33ppi的QVGA LCD屏幕

我记得，08年好像这有个故障。就是卡机。在维基上一查，发现是飞思卡尔驱动的问题。闰年bug，导致08年12月31日那天卡机。官方说把电放干净再等到09年1月1日充上......

就因为那个时候我把我爸给我买的Zune给扔了。

（这个桥段好眼熟，银河护卫队2......星爵干爹......）

我喜爱Zune30赛过喜爱iPod Classic。虽然Zune和iPod的推力差不多，但是我喜欢它的界面。

![](//panzhifei.fun/img/2020/05/05/p2.jpg)

不过，用这个听歌，得准备一个高阻抗耳机。普通耳机......在夜深人静的时候，掏出Zune来一发...首，按下播放键，耳朵爆炸......

这个听歌，白开水，很纯。或者可以说，是酱香型白酒。iPod Classic就是浓香型白酒。

洋垃圾Zune，底噪蛮大的，可能是主板老了吧。

上面是自己的一点看法，不喜勿喷。

所以，重拾旧好，开搞。

# Zune的系统版本

我手头的两个，一个是1.0TEST版，一个是3.3

![](//panzhifei.fun/img/2020/05/05/p3.jpg)

- 1.0TEST版会在开机的时候显示红色的TEST，连接电脑的时候会在计算机（此电脑）显示盘符，可以直接把歌复制进去（没有封面），也可以通过Windows Media Player传输（有封面）。支持UTF－8文字。
- 3.3版的要通过Zune软件传输歌曲视频，不能显示Unicode西文字母以外的文字，包括UTF－8，否则显示口口口。（可以用MP3TAG转换成汉语拼音或者罗马字）

# Zune软件的使用和传输

- 提示：Macintosh用户请移步BootCamp。

因为手持两种设备，传歌是个大问题。安装了Zune软件，就没法给1.0传；卸载Zune软件吧，3.3那个怎么办？

所以，我研究了几个小时，研究出1.0和3.3并存的方法。大概很少人像我一样，有两个。可以参考。Win10的伙伴们可以参考一下，操作方法差不多。

## 3.3版

- 下载安装Zune Software。
- 连接3.3版本的Zune。

![](//panzhifei.fun/img/2020/05/05/p4.jpg)

## 1.0TEST版

- 不要离开Zune Software，断开3.3的连接。
- 如图，在设置里把那个勾去掉。

![](//panzhifei.fun/img/2020/05/05/p5.jpg)

关闭Zune Software，断开网络连接（软断硬断都行，就不能联网），按下图打开

![](//panzhifei.fun/img/2020/05/05/p6.jpg)

![](//panzhifei.fun/img/2020/05/05/p7.jpg)

然后更新驱动程序

![](//panzhifei.fun/img/2020/05/05/p8.jpg)

![](//panzhifei.fun/img/2020/05/05/p9.jpg)

![](//panzhifei.fun/img/2020/05/05/p10.jpg)

可能会提示设备启动失败，没关系，把USB线断开在连一次就好了

还没完，重要的一步来了

搜索“编辑组策略”（Windows10），或者运行 gpedit.msc

![](//panzhifei.fun/img/2020/05/05/p11.jpg)

家庭版的Windows可能没有组策略，在桌面新建一个文本文档，打开，然后把这些粘贴进去

```shell
@echo off

pushd "%~dp0"

dir /b C:\Windows\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~3*.mum >List.txt

dir /b C:\Windows\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~3*.mum >>List.txt

for /f %%i in ('findstr /i . List.txt 2^>nul') do dism /online /norestart /add-package:"C:\Windows\servicing\Packages\%%i"

pause 
```

保存，更改后缀为＊.bat，右键，以管理员身份运行。等CMD窗口滚完了，就好了。

好，打开组策略管理器

![](//panzhifei.fun/img/2020/05/05/p12.jpg)

显示内容里面，设备ID要在控制面板／设备管理器／便携设备／Zune／（右键）属性／详细信息 中的下拉框选择 硬件ID，硬件ID复制那个长的。

完了好了。

![](//panzhifei.fun/img/2020/05/05/p13.jpg)

# Zune的系统升级（模拟服务器3.x的系统升级到3.3）

这里借鉴了Zune贴吧HansonYUE的教程，我重置一遍

[【ZUNE全机型】4.8软件模拟官方服务器刷机/升级教程！](https://tieba.baidu.com/p/4538180873?red_tag=1438151750)

温馨提示：1.x的系统可以不用看了，别做傻事

微软在2016年正式停止了Firmware的服务，就说明官方手段是没的刷机了。

但是我们还有可爱的127.0.0.1啊。

于是乎

- 下载安装Zune Software 4.8（也只有4.8能够将就用了）
- 下载[Zune－Fireware－x86.msi](//download.microsoft.com/download/D/F/C/DFCA346F-B2B2-44B7-803B-262C84673F00/Zune-Firmware-x86.msi)固件文件 
- 用7-zip或者压缩软件提取msi文件里面的文件
- 将提取出来的FirmwareUpdate.xml复制并重命名为zuneprod.xml
- 提取出来的文件可能是没有点号的，文件名可能是DracoBaselineCab，需要自己手动添加一个点，变成DracoBaseline.Cab（这样就不会出现一些错误代码）
- 用记事本编辑zuneprod.xml文档找到 "URL=" 这项并添加内容 "//resources.zune.net/" 至***.cab 之前（例如URL="//resources.zune.net//某.cab"） 并保存
- 下载[Abyss Web Server X1](https://aprelium.com/abyssws/download.php)软件，直接安装，默认路径即可，安装完直接启动软件
- Abyss Web Server X1启动后会弹出网页，语言选英语，用户名密码随意输入，输入完你得记得，跟着弹出登录框再次输入用户名密码，启动服务
- 在DNS服务软件目录下C:\Abyss Web Server\htdocs\建立目录“firmware”，进入firmware目录后分别建“v3_3”和“v4_5”两个目录 (ZUNE HD机型为v4_5，其它都是v3_3)
- 把修改好的zuneprod.xml文档分别复制到C:\Abyss Web Server\htdocs\firmware\v4_5和v3_3目录里
- 把所有之前提取的固件文件***.cab复制到C:\Abyss Web Server\htdocs\目录下。用记事本修改hosts文件（%SystemRoot%\System32\drivers\etc\hosts）在最后一行添加"127.0.0.1 resources.zune.net"。（最后可CMD下ping一下resources.zune.net返回地址是不是127.0.0.1，如果不是检查下Abyss Web Server X1是否运行，hosts文件是否正确）
- 连接Zune（可先硬格）播放至电脑，启动ZUNE软件就能见升级或刷机界面直接正常使用了

![](//panzhifei.fun/img/2020/05/05/p14.jpg)

有四项要修改的

The END.

# 其他

![](//panzhifei.fun/img/2020/05/05/p15.jpg)

3.3的我无法格机，哪位大神可以解释一下

# 其他

Zune的硬盘机很骚包，800mAh的电池，128k的mp3歌能放13个小时（官方数据）。不过，可能有细心的朋友会发现，硬盘只有在切换歌曲的时候会运转，也就是说，从硬盘读取数据，加载到内存里，然后硬盘停止，做到省电。（我试了一下，硬盘机单曲循环可以放15小时，顺序和乱序差不多，8个小时左右，WMALossless格式的歌）

所以，现在网上很少有硬盘机了，都是改卡改电。改CF卡读取快还省电，改大电池续航好。

硬盘很糟糕，加载慢，切歌切快的话会假死。（因为可以听到硬盘读取的声音）这个时候等一下就好了，千万别重启或者关机，重启完会发现歌全没了（读取不了）。（吃过亏）

充电的话，最好插在电脑上充电，电流稳定，充的还饱。

# 后记

Zune也饱受诟病

谢耳朵

![](//panzhifei.fun/img/2020/05/05/p16.jpg)

![](//panzhifei.fun/img/2020/05/05/p17.jpg)

![](//panzhifei.fun/img/2020/05/05/p18.jpg)

额，这到底是什么黑

# 炫耀一番

为了这篇蓄谋已久的文章，我特地把那该死的Mac mini（2010mid）的电脑装了Windows7（只能装win7我也没办法啊）

![](//panzhifei.fun/img/2020/05/05/p19.jpg)

今天装的，OEM系统光盘，正版电话激活

妈妈呀，9102年，Win7快死了还能电话激活

![](//panzhifei.fun/img/2020/05/05/p20.jpg)

![](//panzhifei.fun/img/2020/05/05/p21.jpg)

![](//panzhifei.fun/img/2020/05/05/p22.jpg)

![](//panzhifei.fun/img/2020/05/05/p23.jpg)

![](//panzhifei.fun/img/2020/05/05/p24.jpg)

![](//panzhifei.fun/img/2020/05/05/p25.jpg)

我的Zune们

壁纸是《可塑性记忆》的ED里面的艾拉，自己买的光碟截的图

![](//panzhifei.fun/img/2020/05/05/p26.jpg)

Hello from Seattle

评论区开放，大家多提供建议。

![](//panzhifei.fun/img/2020/05/05/p27.jpg)

2020年2月1日更

琢磨了一下搞明白了3.3的格机方法

就是在开机的时候，出现Zune标的时候按格机键就好了

![](//panzhifei.fun/img/2020/05/05/p28.jpg)

2020-05-04从知乎搬运回我的博客
