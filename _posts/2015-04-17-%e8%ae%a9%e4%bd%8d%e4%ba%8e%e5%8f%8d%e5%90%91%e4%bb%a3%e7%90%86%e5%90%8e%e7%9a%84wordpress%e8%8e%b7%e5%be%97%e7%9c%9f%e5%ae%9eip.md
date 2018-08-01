---
id: 172
title: 让位于反向代理后的wordpress获得真实ip
date: 2015-04-17T21:11:04+00:00
author: 崔 天一
layout: post
guid: https://blog.ctyi.me/?p=172
permalink: /archives/172
categories:
  - 服务器
tags:
  - apache
  - nginx
  - wordpress
  - 反向代理
  - 真实ip
---
由于freeshell使用nginx作为反向代理，导致apache不能获取到客户端的ip，从而wordpress中评论的ip地址都显示为了nginx反向代理的ip。

在apache上安装mod_rpaf插件，将nginx设置的<span class="lang:default decode:true  crayon-inline ">X-Real-IP</span> 变量中的真实ip复制到<span class="lang:default decode:true  crayon-inline ">X-Forwarded-For</span> 变量内：

下载插件：

<pre class="lang:sh decode:true ">wget http://drupion.com/sites/default/files/mod_rpaf-0.6.tar_.gz</pre>

编译安装：

<pre class="lang:sh decode:true ">yum install httpd-devel
tar zxvf mod_rpaf-0.6.tar_.gz
cd mod_rpaf-0.6
apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c</pre>

编辑apache的配置文件：添加一个配置文件

<pre class="lang:sh decode:true ">/etc/httpd/conf.d/mod_rpaf.conf</pre>

&nbsp;

<pre class="lang:apache decode:true">#载入模块
LoadModule rpaf_module modules/mod_rpaf-2.0.so

# mod_rpaf configuration
#打开模块
RPAFenable On
#根据前端设置主机名
RPAFsethostname On
#将前端反向代理的ip填入xxx.xxx.xxx.xxx
RPAFproxy_ips xxx.xxx.xxx.xxx
#将真实X-Forwarded-For变量填入真实ip
RPAFheader X-Forwarded-For</pre>

&nbsp;

但诡异的是，wordpress并不认这个<span class="lang:default decode:true  crayon-inline ">X-Forwarded-For</span> 变量，需要再安装一个叫reverse-proxy-comment-ip-fix的插件，方可获取到真实的客户端ip。