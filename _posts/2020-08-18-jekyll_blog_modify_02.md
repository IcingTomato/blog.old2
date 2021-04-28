---
layout: post
title: "Plan of Jekyll Blog Transfer - Episode 2: Gitalk & Google Analytics"
description: "How to configure Gitalk & Google Analytics on Jekyll Blog?"
comments: false
keywords: "Linux, Ubuntu, Ubuntu16.04, Jekyll, Nginx, Gitalk, Google Analytics"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=461301452&auto=1&height=66"></iframe>

# Gitalk on Jekyll

博客完工了好久，发现没有评论系统，就很不爽

于是乎找了好久找到两个

[Disqus](https://disqus.com/) 和 [Gitalk](https://gitalk.github.io/)

最终选择了Gitalk。

Gitalk 是一个基于 Github Issue 和 Preact 开发的评论插件。它除了支持 Hexo 外，还支持 java，php 等语言开发的博客。

## 使用方法

首先需要到GitHub上去新建一个仓库用于存放评论的内容

![](//panzhifei.fun/img/2020/08/18/01/1.jpg)

![](//panzhifei.fun/img/2020/08/18/01/2.jpg)

其次，在设置中打开issues。（其实这个默认打开的，检查一下吧）

![](//panzhifei.fun/img/2020/08/18/01/3.jpg)

然后就要注册一个[Github Application](https://github.com/settings/applications/new)

![](//panzhifei.fun/img/2020/08/18/01/4.jpg)

注意两个URL就是你网站的域名。应用名称随便写，描述随便写。

完成之后便到了如下页面

![](//panzhifei.fun/img/2020/08/18/01/5.jpg)

把这个填入该填的位置就好了（按照Gitalk的示例填就行）

# Google Analytics for WebSite

[Google Analytics](https://analytics.google.com/)

![](//panzhifei.fun/img/2020/08/18/01/6.jpg)
