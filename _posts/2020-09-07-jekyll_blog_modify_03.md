---
layout: post
title: "Plan of Jekyll Blog Transfer - Episode 3: Move to AWS"
description: "How to configure Jekyll on Ubuntu18.04?"
comments: false
keywords: "Linux, Ubuntu, Ubuntu18.04, Jekyll, Nginx, Gitalk, Google Analytics"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=573583339&auto=1&height=66"></iframe>

# Jekyll on Ubuntu 的二次配置

上次的博客（2020年8月17日-[绵绵葛藟 在河之漘](https://panzhifei.xyz/2020/08/17/%E7%BB%B5%E7%BB%B5%E8%91%9B%E8%97%9F%E5%9C%A8%E6%B2%B3%E4%B9%8B%E6%BC%98/)）里面有很多未解决的事情

比如

![](//panzhifei.fun/img/2020/09/07/01/01.jpg)

搞了半天，原来是Liquid的问题

升级到Jekyll 4可以支持HTML标签，说明可以在Markdown里面嵌入网易云的音乐和B站视频

![](//panzhifei.fun/img/2020/09/07/01/02.jpg)

- 头一个就是自己傻呵呵地 gem update jekyll 之后忘记安装 jekyll-paginate

- 其次，就是 _config.yml 的问题，历史遗留问题

![](//panzhifei.fun/img/2020/09/07/01/03.jpg)

- 最后 jekyll build 就好了

新地址 [http://me.panzhifei.xyz/](http://me.panzhifei.xyz/)

速度改善了很多，虽然服务器在美利坚弗吉尼亚

说了那么多，还是因为域名是在腾讯云买的，又买了阿里云的学生机

这俩鬼打架

心累