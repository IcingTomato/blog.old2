---
layout: post
title: "Plan of Jekyll Blog Transfer - Episode 5: Anglicized & Add SSL"
description: "New Blog"
comments: false
keywords: "Linux, Ubuntu, Ubuntu16.04, Jekyll, Nginx, Gitalk, Google Analytics"
---

# Fix some problem

When I used the new blog template, it occured some problem.

```shell
$ cd <the folder>
$ git clone <repository-address>
$ bundle add webrick rake
$ bundle install --path vendor/cache
$ git pull origin master
$ bundle exec jekyll build -d /var/www/html/
```

First, you need to install some Dependence like `webrick` `rake` `jekyll`.

And then, in my case, I had a PATH problem.

```
Bundler::GemNotFound: Could not find rake-10.3.2 in any of the sources
~/.rvm/gems/ruby-2.0.0-p451/gems/bundler-1.6.2/lib/bundler/spec_set.rb:92:in `block in materialize'
~/.rvm/gems/ruby-2.0.0-p451/gems/bundler-1.6.2/lib/bundler/spec_set.rb:85:in `map!'
~/.rvm/gems/ruby-2.0.0-p451/gems/bundler-1.6.2/lib/bundler/spec_set.rb:85:in `materialize'
~/.rvm/gems/ruby-2.0.0-p451/gems/bundler-1.6.2/lib/bundler/definition.rb:133:in `specs'
~/.rvm/gems/ruby-2.0.0-p451/gems/bundler-1.6.2/lib/bundler/definition.rb:178:in `specs_for'
Show 28 more lines
```

I used `gem install rake` but it was no use fixing the matter.

SO, `bundle install --path vendor/cache` can help you fix the problem.

This command line generally fixes it as that is the more common problem. Basically, my bundler path configuration is messed up. See their [documentation](https://bundler.io/v1.11/man/bundle-config.1.html) (first paragraph) for where to find those configurations and change them manually if needed.

# Blog Anglicized

Ah...

# Enable SSL & HTTPS

Well, I don't want to buy a SSL key because it is very enpensive. So I used the *free key*.

```shell
server {
        # Enable http(80)
	listen 80 default_server;     
	listen [::]:80 default_server;

        # Enable https(443)
	listen 443 ssl default_server;
	listen [::]:443 ssl default_server;

        #ssl on;# Disable SSL, because when it enabled, it blocked http pages.
        ssl_certificate <key-path>.pem;
        ssl_certificate_key <key-path>.key;
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;

	root /var/www/html;

	server_name <domain.name>;

	location / {
		try_files $uri $uri/ =404;
	}

        # Rewrited the 404 page to 200
        error_page 404 =200 /404/index.html;

        location /404.html {
                root /var/www/html/404/;
                internal;
        }        

        # Rewrited the 403 page to 200
        error_page 403 =200 /403/index.html;

        location /403.html {
                root /var/www/html/403/;
                internal;
        }
}
```

