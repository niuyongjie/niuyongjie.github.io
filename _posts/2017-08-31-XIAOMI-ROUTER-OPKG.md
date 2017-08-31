---
title: 小米路由器_opkg包管理工具
tags: [小米路由器,opkg]
grammar_cjkRuby: true
---

[toc]


## opkg软件包管理工具

小米路由器基于openwrt订制而来,但默认没有提供opkg,所以我们需要进行一番改造.

1. 确定路由器cpu架构

> uname -m   #小米路由器3显示mips架构


2. 获取openwrt软件包的地址

```shell
cat /etc/opkg.conf 
#在第一行中得到仓库的地址http://downloads.openwrt.org/barrier_breaker/
```

用浏览器访问上面的地址找到适合的cpu型号的软件包修改/etc/opkg.conf文件的内容如下：

```
src/gz attitude_adjustment_base http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/base
src/gz attitude_adjustment_packages http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/packages/
src/gz attitude_adjustment_luci http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/luci/
src/gz attitude_adjustment_management http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/management/
src/gz attitude_adjustment_oldpackages http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/oldpackages/
src/gz attitude_adjustment_routing http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/routing/
#src/gz openwrt_dist http://openwrt-dist.sourceforge.net/releases/ramips/packages
#src/gz openwrt_dist_luci http://openwrt-dist.sourceforge.net/releases/luci/packages
dest root /data
dest ram /tmp
lists_dir ext /data/var/opkg-lists
option overlay_root /data
arch all 100
arch ramips 200
arch ramips_24kec 300
```

3. 上传opkg二进制文件

由于小米路由器默认没有opkg二进制文件，所以找一份适合的opkg文件上传到小米路由器中。

```
scp opkg username@yoursship:/data  #上传文件
ssh username@yoursship #ssh 登录到小米路由器
cd /data
ln -s opkg /bin #为opkg创建软接
```

4. 更新软件列表

> opkg update

如果遇到无法下载的情况，根据终端提示屏蔽掉/etc/opkg.conf文件中的配置项(在行首添加#号)

## 安装git服务

在我们之前添加的软件仓库中，已经包含了git包，所以可以直接进行安装。

```shell
# 安装libc包
cd /data 
wget http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/base/libc_0.9.33.2-1_ramips_24kec.ipk 
opkg install libc_*.ipk

# 安装git服务
opkg install git

# 为git可执行文件创建软链接
ln -s /data/usr/bin/git-upload-pack /usr/bin/git-upload-pack
ln -s /data/usr/bin/git-upload-archive /usr/bin/git-upload-archive
ln -s /data/usr/bin/git-receive-archive /usr/bin/git-receive-archive
ln -s /data/usr/bin/git /usr/bin/git

```