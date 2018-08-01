---
id: 194
title: 在docker中部署Jenkins和Jenkins-slave并进行持续集成
date: 2015-07-01T20:58:10+00:00
author: 崔 天一
layout: post
guid: https://blog.ctyi.me/?p=194
permalink: /archives/194
nkweb_code_in_head:
  - default
nkweb_Use_Custom_js:
  - default
nkweb_Custom_js:
  - ""
nkweb_Use_Custom_Values:
  - default
nkweb_Custom_Values:
  - ""
nkweb_Use_Custom:
  - 'false'
nkweb_Custom_Code:
  - ""
categories:
  - 服务器
tags:
  - CI
  - docker
  - gitlab
  - Jenkins
  - python
  - 持续集成
  - 编程
---
## 一些对docker的介绍

首先是一点复制自docker官方网站的docker介绍：

> Docker is an open platform for building, shipping and running distributed applications. It gives programmers, development teams and operations engineers the common toolbox they need to take advantage of the distributed and networked nature of modern applications.

说的简单些，docker就是一个利用linux内核中的cgroups进行了资源隔离之后的容器，基于LXC。其实就是一种简化版的虚拟机。可以这么理解，一个进程运行在docker中实际上就是它被docker隔离开了，它看不到docker之外的进程。同时，它所能访问的资源也受到了相应的cgroups的限制。

docker有以下优势：

  1. 创造一个不受干扰的环境
  2. 在docker hub上已经有大量的配置好的镜像，下载就可室友
  3. docker与虚拟机相比更加轻量级

先明确几个概念：

1.images，镜像，即一个系统的磁盘文件，docker使用的镜像是差量的，这就是说，docker会自动在一个镜像上覆盖一个新的layer,每次虚拟机中的文件修改发生在新的layer上。同时，也可以在已有的image上叠加layer构成新的镜像。

2.container，容器，即实实在在运行的虚拟机，container从一个image中启动一个进程，该进程退出后container自动关闭。但对应的新创建的layer不会自动清除，也就是说，仍然可以用<span class="lang:default decode:true  crayon-inline ">docker start $ID</span> 的方法重新启动container。

其余内容请参阅<a href="https://docs.docker.com/" target="_blank">https://docs.docker.com/</a>

## Jenkins

Jenkins是一个持续集成工具，也就是说能执行自动构建、部署、单元测试等功能。

## 安装方法

<a href="https://registry.hub.docker.com/_/jenkins/" target="_blank">Jenkins官方docker</a>

上面那个链接给出了详细的部署方法，只要<span class="lang:default decode:true  crayon-inline ">docker pull jenkins</span> 再执行

<pre class="lang:sh decode:true ">docker run --name myjenkins -d -p 8000:8080 -v /var/jenkins_home jenkins</pre>

一个含有jenkins的container就运行起来了，省去了安装jdk的麻烦。接下来，访问127.0.0.1:8000,在其中的系统管理中搜索安装Docker Plugin插件。值得注意的是，因为在国内无法访问Google，所以check internet 需要很长时间，而且会超时。建议执行

<pre class="lang:sh decode:true ">docker exec -i -t $ID bash</pre>

然后修改/etc/hosts，将www.google.com指向www.baidu.com对应的ip&#8230;&#8230;.

接下来，就是配置Jenkins Slave了。

这里有个问题，Jenkins是通过访问宿主机上的docker API来启动对应的slave的，而Jenkins本身就在container中，因此无法访问宿主机上的docker API,这时，需要在宿主机中的docker配置文件中加入

<pre class="lang:default decode:true ">DOCKER_OPTS="-H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock"</pre>

以让docker监听所有接口。（注意配置防火墙）

然后在宿主机上建立Dockerfile。关键有以下几部分：

  * 安装ssh-server
  * 允许ssh-server登陆
  * 安装openJDK并设置环境变量
  * 设置好locale之类的设置
  * 因为我的项目使用python，还需配置virtualenv，python等内容。以下为完整的Dockerfile

<pre class="lang:default decode:true ">FROM debian:jessie
MAINTAINER Tianyi Cui

COPY sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y supervisor openssh-server \
	python python-pip python-virtualenv \
	openjdk-7-jdk \
	git \
	locales
RUN export LANGUAGE=C.UTF-8 && \
    export LANG=C.UTF-8 && \
    export LC_ALL=C.UTF-8 && \
    locale-gen C.UTF-8 && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales
RUN mkdir /var/run/sshd
RUN echo 'root:yourpassword' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" &gt;&gt; /etc/profile
RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LC_ALL C.UTF-8
ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8
CMD ["/usr/bin/supervisord"]

EXPOSE 22
</pre>

<pre class="lang:default decode:true" title="对应的supervisord.conf">[supervisord]
nodaemon=true
</pre>

然后对其进行docker build . slave就可以了。接下来，在Jenkins的系统设置->云里，并设置好宿主的ip地址等信息，并添加一个docker template，label的作用和nodes里label的作用相同，id填docker build时起的image的name。大功告成！