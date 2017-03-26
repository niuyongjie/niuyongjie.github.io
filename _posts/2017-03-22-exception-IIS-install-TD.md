---
title: 解决TestDirector 8.0 安装找不到IIS服务
tags: [TestDirector,IIS]
grammar_cjkRuby: true
---


## 现象

在安装TestDirector 8.0客户端版本时时报找不到IIS服务,见下图.

![enter description here][1]

## 解决过程

由于我的电脑是新装的电脑,所以:

1. 安装对应系统的补丁集合;如: [win7 sp1 补丁集合][2]
2. 将你本机的IE版本与测试人员使用的IE版本保持一致.
3. 安装 ==.NET Framework== .
4. 打开系统IIS服务.

![enter description here][3]

5. 下载完整版的 ==Test director 8.0 ==
6. 安装客户端插件

![enter description here][4]

7. 以管理员的身份运行 ==TestDirector== .
8. 输入测试人员提供的url.单击Go按钮,程序会自动运行,从服务器中下载必要的组件并安装注册.

> **Note** 
> 1. 在最后一步中可能出现卡住的现象,结束掉任务多运行几次就OK.
> 2. 客户端版的TD不需要安装TD的主程序
> 3. IIS版本过高可能导致报IIS服务找不到
> 4. 话说都什么年代了还用这么老的东西


  [1]: {{ site.baseurl }}/assets/images/iis-not-found.PNG "iis-not-found"
  [2]: http://www.catalog.update.microsoft.com/Search.aspx?q=3125574&tduid=%28fa4978f0834c65ac05dd7c9f5c739c17%29%28256380%29%282459594%29%28TnL5HPStwNw-XtXswafxX3b2inoFekBnuw%29%28%29
  [3]: {{ site.baseurl }}/assets/images/open-iis-server.PNG "open-iis-server"
  [4]: {{ site.baseurl }}/assets/images/install-client-side-plugin.PNG "install-client-side-plugin"
