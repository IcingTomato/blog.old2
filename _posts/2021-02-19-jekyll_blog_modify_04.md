---
layout: post
title: "Plan of Jekyll Blog Transfer - Episode 4: All Done"
description: "Move to Alicloud"
comments: false
keywords: "Linux, Ubuntu, Ubuntu16.04, Jekyll, Nginx, Gitalk, Google Analytics"
---

# 博客空白仓库分支

[点击此处访问](https://github.com/ch1y4/ch1y4.github.io/tree/blank)

# Windows的cmd命令查询指定端口占用的进程并关闭

1. 查找对应的端口占用的进程：`netstat  -aon|findstr "1080"`，找到占用1080端口对应的程序的PID号;

2. 根据PID号找到对应的程序：`tasklist|findstr "PID号"`，找到对应的程序名;

3. 结束该进程：`taskkill /f /t /im "PID号"`.

# GitHub本地仓库配置

```shell
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin 仓库地址
git push -u origin master
```

# GitHub 回退回某个commit

```shell
$ git reset --hard 某个commit id
$ git push -f -u origin master
```

至于我为什么要写这个，因为上传这张博客的时候不知道为啥始终报错。

> There was a YAML syntax error on line 10 column 7 in `<unknown>`: `found a tab character that violate indentation while scanning a plain scalar`.

第十行第七字段是个tag啊！！！！

```yml
---
layout:     post
title:      采采卷耳 不盈顷筐
subtitle:   Jekyll博客完整教程
date:       2021-02-18
author:     千夜chiya
header-img: img/2021/02/18/02/title.jpg
catalog: true
tags:
    - Jekyll
    - Nginx
    - Linux
    - Nano Pi
    - Ubuntu
    - Gitalk
    - Google Analytics
---
```

以前的博客咋都没问题

```yml
---
layout:     post
title:      屡顾尔仆 不输尔载
subtitle:   Jekyll博客迁移计划：Gitalk 插件与 Google Analytics 的配置
date:       2020-08-18
author:     千夜chiya
header-img: img/2020/08/18/01/title.jpg
catalog: true
tags:
    - Jekyll
    - Nginx
    - Linux
    - Nano Pi
    - Ubuntu
    - Gitalk
    - Google Analytics
---
```

本地加载的时候

```yml
Liquid Exception: Liquid syntax error (line 417): Syntax Error in 'assign' - Valid syntax: assign [var] = [source] in /home/zhifei/Documents/ch1y4/_posts/2021-02-18-采采卷耳不盈顷筐.md
```

也不知道是啥情况，放在这慢慢找吧。

# Jekyll博客配置教程

我是LNMP派，因为我不会用Apache配置。

然而静态博客没必要MySQL, MariaDB, PHP。所以我们只安装Jekyll所有必需的依赖项。

```shell
$ sudo apt-get install ruby-full build-essential zlib1g-dev nginx
$ sudo apt-get install gcc g++ make
$ curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn
```

然而Ubuntu 16.04太老了，ruby的版本不支持Jekyll 4。所以我们要手动安装Ruby 3.0.0。

第一步是为Ruby安装一些依赖项。一步一步运行。

```shell
$ sudo apt install curl
$ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

$ sudo apt-get update
$ sudo apt-get install git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn
```

接下来，我们将使用以下三种方法之一安装Ruby。每个都有自己的好处，如今大多数人都喜欢使用rbenv，但是如果您熟悉rvm，也可以按照这些步骤进行操作。我也提供了从源代码安装的说明，但是一般而言，您需要选择rbenv或rvm。

- 方法一：使用rbenv安装。首先安装rbenv，然后安装ruby-build：

```shell
$ cd
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
$ exec $SHELL

$ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
$ echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
$ exec $SHELL

$ rbenv install 3.0.0
$ rbenv global 3.0.0
$ ruby -v
```

- 方法二：RVM安装

```shell
$ sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
$ curl -sSL https://get.rvm.io | bash -s stable
$ source ~/.rvm/scripts/rvm
$ rvm install 3.0.0
$ rvm use 3.0.0 --default
$ ruby -v
```

- 方法三：Ruby源码安装

```shell
$ cd
$ wget http://ftp.ruby-lang.org/pub/ruby/3.0/ruby-3.0.0.tar.gz
$ tar -xzvf ruby-3.0.0.tar.gz
$ cd ruby-3.0.0/
$ ./configure
$ make
$ sudo make install
$ ruby -v
```

Ruby服务器在国外，我的博客服务器在国内，所以换个Ruby源

```shell
$ gem source -r https://rubygems.org/
$ gem source --add https://gems.ruby-china.com/
$ gem source -u
```

最后一步是安装Bundler

```shell
$ gem install bundler jekyll github-pages jekyll-paginate webrick
```

安装完之后就可以将博客从`GitHub`或`Gitee`上`git clone`下来了。

接着完成对`nginx`的配置

安装`nginx`

```shell
$ sudo apt-get install nginx
```

然后定位到`nginx`的配置文件：

```shell
$ sudo vim /etc/nginx/sites-enabled/default
```

配置文件在下面：

```shell
pi@ubuntu:~$ cat /etc/nginx/sites-enabled/default 
server {
	# 监听80端口，我嫌麻烦就懒得加SSL了
	listen 80 default_server;
	listen [::]:80 default_server;
  # 网页在本地的根目录
	root /var/www/html;
  # 显示的主页
	index index.html;
  # 你的域名
	server_name domain.yours;
  # 404，403配置文件
  # 主要目的是当出现404或403时直接回显200
	error_page 404 =200 /404.html;
        # 404
        location /404.html {
                root /var/www/html/;
                internal;
        }        
        # 403
        error_page 403 =200 /offline.html;
        # 404
        location /offline.html {
                root /var/www/html/;
                internal;
        }        
}
```

保存好之后重启`nginx`

```shell
$ sudo systemctl restart nginx
```

# 最终使用

如果配置好nginx和Jekyll的话

```shell
$ cd 文件夹
$ git clone 仓库地址
$ git pull origin master
$ jekyll build -d /var/www/html/
```

# 致谢

1. 这个模板是从这里 [Hux](https://github.com/Huxpro/huxpro.github.io) 和 [BY](https://github.com/qiubaiying/qiubaiying.github.io) fork 的, 感谢这两位作者。 
2. 感谢 Jekyll、Github Pages 和 Bootstrap!

# License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="http://panzhifei.fun/img/license/cc.png" /></a><br />本博客采用<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">知识共享署名-相同方式共享 4.0 国际许可协议</a>进行许可。

