---
title: 如何从Chrome应用商店下载插件
tags: [Chrome,插件,下载,crx]
grammar_cjkRuby: true
---

## 背景

最近遇到了一个问题:我需要将Chrome浏览器的插件共享给别人,然而从自己的浏览器插件管理页面进行打包插件报找不到 ==Manifest== 文件.

![enter description here][1]

去搜索引擎搜索,推送的版本都比较低,不符合要求

通过一番折腾终于从Chrome 应用商店下载下来了以 ==crx== 为后缀的插件文件.

## 具体的过程

- Chrome 浏览器在安装插件时首先会将插件下载到本地,然后安装插件,最后删除下载的插件文件
- 通过Chrome Developer Tools工具获得Chrome浏览器关于插件的两个重要的URL地址,分别是:

```
插件的详情页URL(用来找到该插件的id):
https://chrome.google.com/webstore/ajax/detail?hl=zh-
CN&gl=CN&pv=20170206&mce=atf%2Ceed%2Cpii%2Crtr%2Crlb%2Cgtc%2Chcn%2Csvp
%2Cwtd%2Cc3d%2Cncr%2Cctm%2Cac%2Chot%2Ceuf%2Cmac%2Cfcf%2Crma%2Cigb
%2Cpot%2Cevt%2Crae%2Cshr%2Cesl%2Cirt%2Cscm%2Cqso%2Chrb%2Cdda&
id=imilbobhamcfahccagbncamhpnbkaenm
&container=CHROME&_reqid=9032548&rt=j
```

```
下载插件的URL(用来下载后缀为 ==crx== 的插件):
https://clients2.google.com/service/update2/crx?
response=redirect&prodversion=49.0&x=
id%3Dimilbobhamcfahccagbncamhpnbkaenm%
26installsource%3Dondemand%26uc
```

- 将详情页中的URL替换到下载插件URL中 ==id%3Dxxxxx%== 之间的内容,就可以下载到插件的安装文件了.

  [1]: {{site.baseurl}}/assets/images/Chrome插件管理页面.jpg "Chrome 插件管理界面"
