---
id: 106
title: 在USTC freeshell上配置snmp使用监控宝
date: 2014-08-13T15:08:14+00:00
author: 崔 天一
layout: post
guid: http://blog.ctyi.me/?p=106
permalink: /archives/106
categories:
  - 服务器
tags:
  - snmp
  - USTC
  - VPS
  - 中科大
  - 折腾
  - 服务器
  - 监控宝
  - 运维
---
刚被中科大录取没几天，便发现中科大提供freeshell服务，便试图在上面配置监控宝。

我使用的发行版是centos 6， 内置了net-snmp，只需创建一个账户并配置权限即可。

1.编辑配置文件<span class="lang:default decode:true  crayon-inline ">/etc/snmp/snmpd.conf</span> ，添加以下内容：

<pre class="lang:default decode:true ">rouser kwxgd auth
createUser kwxgd MD5 mypassword</pre>

意思是：给账号kwxdg只读的权限，并需要验证。

创建账号kwxgd，密码使用md5加密，密码为passowrd

2.启动服务

<pre class="lang:default decode:true ">service snmpd start</pre>

3.设置开机启动

<pre class="lang:default decode:true ">chkconfig snmpd on</pre>

4.在ustc freeshell里添加端口映射：

[<img class="alignnone size-medium wp-image-107" src="http://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813145544-300x53.png" alt="端口映射" width="300" height="53" srcset="https://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813145544-300x53.png 300w, https://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813145544.png 474w" sizes="(max-width: 300px) 85vw, 300px" />](http://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813145544.png)

5.在监控宝中添加相关项目：

[<img class="alignnone wp-image-108 size-large" src="http://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813150131-1024x482.png" alt="监控宝" width="474" height="223" srcset="https://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813150131-1024x482.png 1024w, https://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813150131-300x141.png 300w, https://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813150131.png 1366w" sizes="(max-width: 474px) 85vw, 474px" />](http://blog.ctyi.me/wp-content/uploads/2014/08/QQ截图20140813150131.png)

&nbsp;

&nbsp;

然后就完成了。

&nbsp;