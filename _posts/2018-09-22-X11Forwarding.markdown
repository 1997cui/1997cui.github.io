---
layout: post
title:  "在WSL里面使用中文"
date:   2018-09-22 18:10:13 -0700
categories: 技术
tags:
 - Linux
 - WSL
 - Win10
 - X11
---

我的WSL发行版是debian，首先需要安装中文字体`fonts-noto-cjk`。

然后装中文输入法`fcitx`, `fcitx-pinyin`, `fcitx-googlepinyin`。

然后打开`.bashrc`或者`.zshrc`,在其中加入
``` sh
export LC_ALL="zh_CN.UTF-8"
export DISPLAY=:0
export QT_IM_MODULE=fcitx
export GTK_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```
然后启动`fcitx`，运行`fcitx-config-gtk3`把Google Pinyin添加进输入法列表就好啦~