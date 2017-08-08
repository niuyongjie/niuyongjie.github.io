---
title: 小米路由器_折腾记录
tags: [小米路由器,记录]
grammar_cjkRuby: true
---

[toc]


## 获取路由器管理权限

### 刷开发版ROM

1.  在 [miwifi 官网][1] 的下载页面中的->ROM页面->下载开发版包
2.  在浏览器中输入miwifi.com进入路由器的管理界面
3.  找到常用设置->系统状态->手动升级->选择下载好的开发包进行升级
4.  升级过程中路由起会重启,导致断网,刷新无线网列表,找到重启后的路由器连接即可.

### 开启SSH工具

![开启SSH工具][2]

1. 在 [官网][3] 下载SSH工具包,记录root密码
1. 将下载的工具包bin文件复制到U盘（FAT/FAT32格式）的根目录下,保证文件名为miwifi_ssh.bin；
2. 断开小米路由器的电源,将U盘插入USB接口；
3. 按住reset按钮之后重新接入电源,指示灯变为黄色闪烁状态即可松开reset键；
4. 等待3-5秒后安装完成之后,小米路由器会自动重启;


### 登录SSH并修改登录密码

```
# 在终端中通过SSH登录路由器
ssh root@192.168.31.1
# 输入之前记录的root密码
# 修改root密码,方便记忆,在下次SSH登录时使用修改后的密码
passwd [自定义的密码]
```


> NOTE
> 开启SSH前提是需要刷开发版ROM

### 获取根目录的读写权限

小米路由器虽然开放了root权限,但根目录是只读的,所以需要重新挂载根目录,赋予读写权限：

> mount -o remount -rw /

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


  [1]: http://www1.miwifi.com/miwifi_download.html
  [2]: https://www.github.com/niuyongjie/imageBed/raw/master/1502056412406.jpg
  [3]: http://d.miwifi.com/rom/ssh
