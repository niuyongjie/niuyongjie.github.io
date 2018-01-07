---
title: 小米路由器安装Git服务
tags: [小米路由器,Git]
grammar_cjkRuby: true
---


在之前的博文中已经安装了opkg软件包管理器,并添加了相应的软件仓库。
现在我们通过该仓库安装git服务。

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
ln -s /data/usr/bin/git /bin/git-upload-pack
ln -s /data/usr/bin/git /bin/git-upload-archive
ln -s /data/usr/bin/git /bin/git-receive-archive
ln -s /data/usr/bin/git /bin/git-shell
ln -s /data/usr/bin/git /usr/bin/git
```

是不是很简单？
当然，有余力的同学可以通过交叉编译来生成可用的安装包，再进行安装。
至此，Git 服务已经安装完成，你的路由器现在就是一个小型的 Git 服务器。你可以新建个目录，运行 git init 来初始仓库，或者直接将 project.git 文件夹复制到路由器里，并通过以下的 url 来 clone 仓库

```shell
git clone root@routerip:/gitRepo_path.git
```

Have fun!
