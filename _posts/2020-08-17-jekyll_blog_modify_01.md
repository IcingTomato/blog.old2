---
layout: post
title: "Plan of Jekyll Blog Transfer - Episode 1: Jekyll on Ubuntu & Nginx"
description: "How to configure Jekyll on Ubuntu & Nginx?"
comments: false
keywords: "Linux, Ubuntu, Ubuntu16.04, Jekyll, Nginx"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=461301452&auto=1&height=66"></iframe>

# Jekyll on Ubuntu

## Jekyll Quickstart

原链接[Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)

在安装Jekyll之前，我们需要确保拥有所有必需的依赖项。

```shell
$ sudo apt-get install ruby-full build-essential zlib1g-dev
```

最好避免以root用户身份安装Ruby Gems。因此，我们需要为您的用户帐户设置一个gem安装目录。以下命令将环境变量添加到您的【~/.bashrc】文件中，以配置gem安装路径。立即运行它们：

```shell
$ echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
$ echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
$ echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
$ source ~/.bashrc
```

安装Jekyll：

```shell
$ gem install jekyll bundler
```

最后，从[ch1y4/ch1y4.github.io](https://github.com/ch1y4/ch1y4.github.io)上 git clone

```shell
$ git clone https://github.com/ch1y4/ch1y4.github.io.git
$ cd ch1y4.github.io
$ jekyll serve
```

然后就可以在本地[http://localhost:4000](http://localhost:4000)看到了。

## Liquid warning

如果按照上面这样配置，一定看不到自己的博客。

![](//panzhifei.fun/img/2020/08/17/01/01.jpg)

只是因为Jekyll4的谜之调教。

所以要降级

```shell
$ gem uninstall jekyll
```

然后安装Jekyll3.1.3

```shell
$ gem install jekyll -v 3.1.3
```

最后，缺啥装啥

## Host to 0.0.0.0

完成以上步骤的时候，还不能通过外网访问,而且强制4000端口

换端口

```shell
$ jekyll serve --port 4001
```

上公网

```shell
$ jekyll serve -w --host=0.0.0.0
```

换端口又上公网

诶，还没输入呢

# 建立Nginx代理

由于Jekyll在端口4000上运行，因此要求访问者将端口添加到URL中，这不是很好。我们将安装Nginx，它将把请求从端口80转发到4000。

首先，安装nginx

```shell
$ sudo apt-get install nginx
$ sudo nano /etc/nginx/conf.d/jekyll.conf
```

现在，用喜欢的文本编辑器（nano）编辑/etc/nginx/conf.d/jekyll.conf并粘贴以下内容：

```shell
server {
    listen 80;
    server_name 你的域名;
    location / {
        proxy_pass http://localhost:4000;
    }
}
```

![](//panzhifei.fun/img/2020/08/17/01/02.jpg)

执行以下操作以重新启动Nginx：

```shell
$ jekyll serve --detach
$ sudo systemctl restart nginx
```

# 彩蛋

<script type="text/javascript" src="//rf.revolvermaps.com/0/0/6.js?i=5519oi3k6f4&amp;m=7&amp;c=e63100&amp;cr1=ffffff&amp;f=arial&amp;l=0&amp;bv=90&amp;lx=-420&amp;ly=420&amp;hi=20&amp;he=7&amp;hc=a8ddff&amp;rs=80" async="async"></script>
