---
title: 小米路由器_获取管理权限
tags: [小米路由器,root,ssh]
grammar_cjkRuby: true
---

[toc]


## 刷开发版ROM

1.  在 [miwifi 官网][1] 的下载页面中的->ROM页面->下载开发版包
2.  在浏览器中输入miwifi.com进入路由器的管理界面
3.  找到常用设置->系统状态->手动升级->选择下载好的开发包进行升级
4.  升级过程中路由起会重启,导致断网,刷新无线网列表,找到重启后的路由器连接即可.

## 开启SSH工具

![开启SSH工具][2]

1. 在 [官网][3] 下载SSH工具包,记录root密码
1. 将下载的工具包bin文件复制到U盘（FAT/FAT32格式）的根目录下,保证文件名为miwifi_ssh.bin；
2. 断开小米路由器的电源,将U盘插入USB接口；
3. 按住reset按钮之后重新接入电源,指示灯变为黄色闪烁状态即可松开reset键；
4. 等待3-5秒后安装完成之后,小米路由器会自动重启;


## 登录SSH并修改登录密码

```
# 在终端中通过SSH登录路由器
ssh root@192.168.31.1
# 输入之前记录的root密码
# 修改root密码,方便记忆,在下次SSH登录时使用修改后的密码
passwd [自定义的密码]
```


> NOTE
> 开启SSH前提是需要刷开发版ROM

## 获取根目录的读写权限

小米路由器虽然开放了root权限,但根目录是只读的,所以需要重新挂载根目录,赋予读写权限：

> mount -o remount -rw /


  [1]: http://www1.miwifi.com/miwifi_download.html
  [2]: https://www.github.com/niuyongjie/imageBed/raw/master/1502056412406.jpg
  [3]: http://d.miwifi.com/rom/ssh
