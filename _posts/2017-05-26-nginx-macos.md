---
layout: post
title: "解决Nginx在mac下防火墙问题"
description: ""
category: 
tags: [nginx, macos]
---

##问题
Mac下安装nginx后，本机通过127.0.0.1能正常访问。但是局域网内别的主机通过ip如192.168.0.10访问，就会被防火墙挡住。关闭防护墙后访问正常。

* 在访问墙配置中，加入nginx允许访问列表，发现无效。（注意如果已经加入的话，要在去掉）
* 执行命令
{% highlight shell %} 
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /usr/local/nginx/sbin/nginx
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --unblockapp /usr/local/nginx/sbin/nginx
{% endhighlight %}

* 检查ngnix是否已经加入列表：
{% highlight shell %} 
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --list
{% endhighlight %}

* 重启ngix(不要用reload)：
{% highlight shell %}
sudo /usr/local/nginx/sbin/nginx -s stop
sudo /usr/local/nginx/sbin/nginx
{% endhighlight %}
