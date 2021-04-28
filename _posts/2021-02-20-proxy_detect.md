---
layout: post
title: "How to detect the Proxy when the user is using web browser？"
description: "Haha, it doesn't matter."
comments: false
keywords: "Proxy"
---

纯前端是无法判断的，单纯的后端，如果采用了透明代理(隐藏了真实IP，具备匿名功能)，也难以识别。

不过可以通过Websocket的bufferedAmount来探测用户是否采用了代理，这个代理可能是本地代理，也可能是远程代理。

大致思路是:

1. Client通过Websocket与Server建立连接；
2. Server 监听到connect事件后，将本次TPC的window size设置为0这也就意味着Client无法继续将数据包传给Server；
3. Client 使用websocket.send()持续发送几个包；
4. 在Client.上观察websocket. bufferedAmount值，如果过了一会儿，这个值一直在增大，说明无代理，否则存在代理。

为啥可以通过这个值来判断呢?这是因为代理工具一般不会转发TCP的设置，也就是说，开启了代理的Client发出的包会被代理给吃掉。算是一个不错的策略。

# 推荐几个博客

都是瞎折腾小玩意儿的，没事干可以参观参观。

[Molly Sophia的小世界](https://momosan.cc/)

[module ZephRay;](https://zephray.me/)

