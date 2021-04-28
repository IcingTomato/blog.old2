---
layout: post
title: "How to Push a Cover-available Book to Kindle?"
description: "To repair the non-cover problem"
comments: false
keywords: "Kindle"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=461301452&auto=1&height=66"></iframe>

# 解决Kindle邮箱推送不显示封面的问题

由于我们推送的mobi文件一般都是KF8+Mobi6的文件（这也是calibre默认的转换成mobi）的方式。

这些文件被亚马逊推送过来后有一部分不显示封面的，用Kindle Previewer打开的话书籍信息的文件格式显示“KF8”，那些显示封面的格式是“mobi”

我们在Calibre安装KindleUnpack插件，在插件里面找到它，安装之，然后选择那些邮箱推送不显示封面的书籍，按图片所示的。把书“切割”成mobi6和KF8格式

然后我们得到两个文件。一个后缀为mobi，一个后缀为azw3.

把mobi格式的发到邮箱，应该有封面啦

