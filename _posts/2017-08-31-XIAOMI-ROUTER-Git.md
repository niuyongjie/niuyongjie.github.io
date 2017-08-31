---
title: 小米路由器安装Git服务
tags: [小米路由器,Git]
grammar_cjkRuby: true
---


在之前的博文中已经安装了opkg软件包管理器,并添加了相应的软件仓库，该已经包含了git包，所以可以直接进行安装。

## 安装libc包

```shell?linenums
cd /data 
wget http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/base/libc_0.9.33.2-1_ramips_24kec.ipk 
opkg install libc_*.ipk
```

## 安装git服务

```shell?linenums
opkg install git
```

## 创建软连接

```shell?linenums
ln -s /data/usr/bin/git-upload-pack /usr/bin/git-upload-pack
ln -s /data/usr/bin/git-upload-archive /usr/bin/git-upload-archive
ln -s /data/usr/bin/git-receive-archive /usr/bin/git-receive-archive
ln -s /data/usr/bin/git /usr/bin/git
```