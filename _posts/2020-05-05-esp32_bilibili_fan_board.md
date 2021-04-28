---
layout: post
title: "Let's Build a Bilibili Fan Monitor by ESP32"
description: "ESP32 is very powerful!"
comments: false
keywords: "Bilibili Fan Monitor, ESP32, Arduino"
---

<iframe height=400 width=600 src="//player.bilibili.com/player.html?aid=97006654&bvid=BV1H7411d7k6&cid=165601756&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

转自 [用Arduino玩转掌控板(ESP32)：B站粉丝计数器](https://mp.weixin.qq.com/s/RMPYPJJm5cRrnkXm7bzmxA)
原创 铁熊熊熊熊 铁熊玩创客 2月13日

众所周知，掌控板在创客教育中用的非常广泛，它是一块基于 ESP32 的学习开发板。大家对掌控板编程，用的比较多的都是图形化编程的方式，比如 mPython、Mind+ 等。但是，既然掌控板是基于 ESP32 芯片的，所以我们也可以用 Arduino 软件对其编程。所以，有时间的话，我准备给大家分享一系列用 Arduino 代码对掌控板（ESP32）编程的教程：用 Arduino 玩转掌控版(ESP32)系列

本期给大家带来的是：B 粉计数器（B站粉丝计数器）。

![](//panzhifei.fun/img/2020/05/05/03/title.jpg)

# 前言

如果大家有在玩一些自媒体平台的话，比如微信公众号、B站、知乎、抖音等，那么相信大家对自己的粉丝数、阅读数或者播放量等相关的数据会比较关注，但是每次手动去查看又比较麻烦。

那么有没有简单一些的方法呢？在创客技术宅眼里，万物皆可自动化！

今天就以 B 站为例，手把手教大家做一个桌面 B 站粉丝计数器！为什么是 B 站呢？因为 B 站做起来最简单啊……（哭……）

先来看一下效果，我用 Arduino 软件分别将程序上传至掌控板（ESP32）和 NodeMCU（ESP8266），看到的效果基本是一样的。本来还想做个外壳的，无奈被疫情隔离在家，设备不多，只能做个简易版了，大家将就看看吧。

![](//panzhifei.fun/img/2020/05/05/03/p1.JPG)

![](//panzhifei.fun/img/2020/05/05/03/p2.JPG)

纳尼！粉丝数竟然那么少！丢脸丢脸，还不赶紧三连支持一下喽~

![](//panzhifei.fun/img/2020/05/05/03/p3.JPG)

干啥啥不行，骗粉第一名！

下面开始正式教程。

# 获取 B 站 API

首先用谷歌浏览器（推荐）打开 B 站个人主页，如下图所示，重点关注我圈出来的几个地方，分别是：关注数、粉丝数、点赞数、播放分数，这几个数据的含义，大家一看就明白了，就不解释了。另外还要关注右下角的 UID，这是一串数字，在 B 站中就是你的唯一 ID，这个数字很重要，后面会用到。

![](//panzhifei.fun/img/2020/05/05/03/p4.JPG)

然后在键盘上按下 F12 或者 Ctrl+Shift+I 进入浏览器调试模式，刷新一下 B 站个人主页，然后就会在 Network（网络）标签页下看到一堆返回的数据，从中我们可以看到数据请求的方法（比如 GET），以及对应的 Domain（网址域名）。这里我们要重点关注几行数据，那就是 Domain 为 api.bilibili.com 的几行，下图中我已经圈出来了。

![](//panzhifei.fun/img/2020/05/05/03/p5.JPG)

我们逐一点进去排查，切换到 Response 标签页，在这里我们看到了 2 个熟悉的数据：following（102）和 follower（133），这不正是我们在 B 站个人主页看到的我的关注数（102）和粉丝数（133）么？

![](//panzhifei.fun/img/2020/05/05/03/p6.JPG)

我们在切换到 Headers 标签页，看到请求的网址（Request URL）如下，请求方法为 GET。

![](//panzhifei.fun/img/2020/05/05/03/p7.JPG)

我们将这个网址复制出来观察一下：

```shell
https://api.bilibili.com/x/relation/stat?vmid=224425204&jsonp=jsonp&callback=__jp4
```

其中有一段 vmid=224425204，这后面的数字，不正是我们前面提到的 UID 么？后面的 jsonp、callback 应该是对应的一些回调函数，我们将这些删除，只保留前面部分：

```shell
https://api.bilibili.com/x/relation/stat?vmid=224425204
```

并将它复制到浏览器地址栏去访问一下，看到什么了？是不是只留下一堆最简单的数据，里面包含了我们的关注数与粉丝数？而且这对数据是 JSON 格式的。

![](//panzhifei.fun/img/2020/05/05/03/p8.JPG)

我们将这些数据格式化一下，方便我们查看。这里使用了 VS Code，或者你也可以使用网上其他的 JSON 在线格式化工具，这里不展开了。

![](//panzhifei.fun/img/2020/05/05/03/p9.JPG)

同样的方法，我们去查一下播放数和获赞数在哪里可以查到。

相信你很快就找到了，如下图所示，先找到数据位置：

![](//panzhifei.fun/img/2020/05/05/03/p10.JPG)

再查看相应的 API 网址：

```shell
https://api.bilibili.com/x/space/upstat?mid=224425204&jsonp=jsonp&callback=__jp5
```

![](//panzhifei.fun/img/2020/05/05/03/p11.JPG)

将末尾无关参数删除后：

```shell
https://api.bilibili.com/x/space/upstat?mid=224425204
```

然后再将这个网址在浏览器中打开，我们就看到了熟悉的播放数（view：9047）和获赞数（likes：57）。

![](//panzhifei.fun/img/2020/05/05/03/p12.JPG)

在 VS Code 中将数据格式化，方便查看。

![](//panzhifei.fun/img/2020/05/05/03/p13.JPG)

# 代码编写

## 联网设置

要去获取 B 站的数据，当然要联网啦。我们在程序的最开头，引入一堆联网相关的头文件。这里有一个比较特殊的地方，就是我们同时引入了 ESP32 和 ESP8266 对应的头文件，这样在编译程序的时候，就会根据所选择的的开发板，自动编译对应部分，而不会报错，做到了一套程序兼容两种开发板（ESP32 和 ESP8266）的目的。

```cpp
#if defined(ESP32)
  #include <WiFi.h>
  #include <HTTPClient.h>
#elif defined(ESP8266)
  #include <ESP8266WiFi.h>
  #include <ESP8266HTTPClient.h>
#else
  #error "Please check your mode setting,it must be esp8266 or esp32."
#endif

#include <Wire.h>

// Wi-Fi
const char *ssid = "wifi_name";
const char *password = "wifi_password";

void setup()
{
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected");
}

void loop()
{
}
```

既然要联网，就需要定义你的网络名称和密码，对应修改就行：

```cpp
const char *ssid = "wifi_name";
const char *password = "wifi_password";
```

上面连接 Wi-Fi 的程序，就不展开了，基本是标准写法，在 WiFi 这个库里，找一下例程复制一下就行。

## 获取粉丝数

连接上网络之后，就可以去获取粉丝数了，除了上面已经引入的头文件 HTTPClient，这个库文件可以用来获取网站上的数据。我们还需要用到的 ArduinoJson 这个 JSON 解析库，可以用来解析网站返回的 JSON 数据，并且初始化一个 JSON 解析对象 jsonBuffer。

> ArduinoJson 目前比较流行的有两个版本：V5 和 V6，V5 比较经典和稳定，V6 比较新。两个版本使用起来稍有差异，博主这里使用的是 V5 版本。

```cpp
#include <ArduinoJson.h>

DynamicJsonBuffer jsonBuffer(256); // ArduinoJson V5
```

另外，我们还需要定义 API 的网址、以及初始化粉丝数，单独拎出来是方便大家修改。注意，这里我们网址的访问方式为 http，而不是 https，因为 https 的话，代码会复杂一些。

```cpp
// bilibili api: follower, view, likes
String UID = "224425204";
String followerUrl = "//api.bilibili.com/x/relation/stat?vmid=" + UID; // 粉丝数

long follower = 0; // 粉丝数
```

然后再写一个获取粉丝数的函数 getFollower(String url)，只要传入对应的 API 网址，就能利用 HTTPClient 中的 GET 方法，获取相应的数据，然后再用 ArduinoJson 库进行解析。

```cpp
void getFollower(String url)
{
  HTTPClient http;
  http.begin(url);

  int httpCode = http.GET();
  Serial.printf("[HTTP] GET... code: %d\n", httpCode);

  if (httpCode == 200)
  {
    Serial.println("Get OK");
    String resBuff = http.getString();

    // ---------- ArduinoJson V5 ----------
    JsonObject &root = jsonBuffer.parseObject(resBuff);
    if (!root.success())
    {
      Serial.println("parseObject() failed");
      return;
    }

    follower = root["data"]["follower"];
    Serial.print("Fans: ");
    Serial.println(follower);
  } else {
    Serial.printf("[HTTP] GET... failed, error: %d\n", httpCode);
  }

  http.end();
}
```

最后再在 setup() 中调用一下，看看效果：

```cpp
void setup()
{
  // other setup codes ...
  getFollower(followerUrl);
}
```

打开 Arduino 串口监视器，返回数据正常，说明成功了。

![](//panzhifei.fun/img/2020/05/05/03/p14.JPG)

## 获取播放数与获赞数

这个与获取粉丝数的原理一样，不再赘述，直接看代码：

```cpp
// bilibili api: follower, view, likes
String UID = "224425204";
String followerUrl = "//api.bilibili.com/x/relation/stat?vmid=" + UID;   // 粉丝数
String viewAndLikesUrl = "//api.bilibili.com/x/space/upstat?mid=" + UID; // 播放数、点赞数

long follower = 0; // 粉丝数
long view = 0; // 播放数
long likes = 0; // 获赞数

void setup()
{
  // other setup codes ...
  getFollower(followerUrl);
  getViewAndLikes(viewAndLikesUrl);
}

void getViewAndLikes(String url)
{
  HTTPClient http;
  http.begin(url);

  int httpCode = http.GET();
  Serial.printf("[HTTP] GET... code: %d\n", httpCode);

  if (httpCode == 200)
  {
    Serial.println("Get OK");
    String resBuff = http.getString();

    // ---------- ArduinoJson V5 ----------
    JsonObject &root = jsonBuffer.parseObject(resBuff);
    if (!root.success())
    {
      Serial.println("parseObject() failed");
      return;
    }

    likes = root["data"]["likes"];
    view = root["data"]["archive"]["view"];
    Serial.print("Likes: ");
    Serial.println(likes);
    Serial.print("View: ");
    Serial.println(view);
  } else {
    Serial.printf("[HTTP] GET... failed, error: %d\n", httpCode);
  }

  http.end();
}
```

打开 Arduino 串口监视器，返回数据正常，说明成功了。

![](//panzhifei.fun/img/2020/05/05/03/p15.JPG)

## OLED屏：数据显示

获取到数据之后，我们总不能一直在串口监视器里面查看吧，所以我们利用一个 OLED 12864 屏幕，将数据显示到屏幕上。代码如下：

```cpp
#include <U8g2lib.h>

// 1.3' OLED12864
U8G2_SH1106_128X64_NONAME_F_HW_I2C u8g2(U8G2_R0, U8X8_PIN_NONE);
// 0.96' OLED12864
//U8G2_SSD1306_128X64_NONAME_F_HW_I2C u8g2(U8G2_R0, U8X8_PIN_NONE);

void setup()
{
  // other setup codes ...
  u8g2.begin();
  u8g2.enableUTF8Print();
  u8g2.setFont(u8g2_font_wqy12_t_gb2312b);
  u8g2.setFontPosTop();
  u8g2.clearDisplay();
}

void loop()
{
  u8g2.firstPage();
  do
  {
    display(follower, likes, view);
  } while (u8g2.nextPage());
}

void display(long follower, long likes, long view)
{
  u8g2.clearDisplay();
  u8g2.setCursor(5, 2);
  u8g2.print("B站粉丝计数器");
  u8g2.setCursor(5, 20);
  u8g2.print("粉丝数：" + String(follower));
  u8g2.setCursor(5, 36);
  u8g2.print("获赞数：" + String(likes));
  u8g2.setCursor(5, 52);
  u8g2.print("播放数：" + String(view));
}
```

这里我们用到了 u8g2 库，它是专门用来控制各种显示屏的。在 setup() 中设置了相应的显示参数，定义了一个显示函数 display(long follower, long likes, long view)，可以同时传入相应的数据，并显示出来。然后在 loop() 中调用，看看显示效果。

![](//panzhifei.fun/img/2020/05/05/03/p16.JPG)

## 定时器：定时获取数据

有了前面的步骤，我们已经可以正常获取数据并且显示数据了，但是你们可能会问：为什么前面调试时把获取数据的函数放在 setup() 中呢？而不是 loop() 中呢？这样每次程序开机只能读取一次，岂不是太麻烦了？放在 loop() 不就可以不断读取并且更新了么？

不是这样的，如果我们放在 loop() 中，不做其他干预，不断去读取的话，就会由于访问频率太高，触发 B 站的保护机制。不信你就不断刷新 B 站的某个 API 地址试试，相信你一定会看到如下“该页面无法访问”的页面。

![](//panzhifei.fun/img/2020/05/05/03/p17.JPG)

所以呢，我们就需要定时器，隔一段时间去获取一次数据，而且我们也不是大 V，数据变化不会很快，所以每隔 10 分钟去获取一次数据就绰绰有余了。直接看代码：

```cpp
#include <Ticker.h>

Ticker timer;
int count = 0;
boolean flag = true;

void setup()
{
  // other setup codes ...
  timer.attach(600, timerCallback); // 每隔10min
}

void loop()
{
  while (flag)
  {
    if (count == 0)
    {
      // display data
      Serial.println("count = 0, display data");
      u8g2.firstPage();
      do
      {
        display(follower, likes, view);
      } while (u8g2.nextPage());
      flag = false;
    } else if (count == 1) {
      // get follower
      Serial.println("count = 1, get follower");
      getFollower(followerUrl);
      flag = false;
    } else if (count == 2) {
      // get view and likes
      Serial.println("count = 2, get view and likes");
      getViewAndLikes(viewAndLikesUrl);
      flag = false;
    }
  }
}

void timerCallback()
{
  count++;
  if (count == 3)
  {
    count = 0;
  }
  flag = true;
}
```

我们使用了 ESP32 和 ESP8266 自带的定时器库 Ticker。设置一个 count 变量，根据 count = 0、1、2 分别做不同的工作：显示屏刷新数据、读取粉丝数、读取播放数和获赞数。用 flag 变量去标记是否执行相应的功能。这两个参数在定时器回调函数 timerCallback() 每隔 10 分钟就会改变一次，然后就会在 loop() 中触发相应的功能。

至此，B站粉丝计数器就制作完成了，最终效果，大家可以在文章开头看一看。

# 附：掌控板图形程序

![](//panzhifei.fun/img/2020/05/05/03/p18.JPG)

# 代码下载

关注本公众号“铁熊玩创客”，回复“B站”获取完整代码，三连支持一下喽。

![](//panzhifei.fun/img/2020/05/05/03/p19.JPG)

# 补记

此文章转载自[用Arduino玩转掌控板(ESP32)：B站粉丝计数器](https://mp.weixin.qq.com/s/RMPYPJJm5cRrnkXm7bzmxA)

原创 铁熊熊熊熊 铁熊玩创客 2月13日

请关注原作者公众号及B站账号

感谢原作者的大力支持

这是我的[代码](https://github.com/ch1y4/ESP/blob/master/ESP8266/bilibiliFans/bilibiliFans.ino)

如有错讹，敬请斧正
