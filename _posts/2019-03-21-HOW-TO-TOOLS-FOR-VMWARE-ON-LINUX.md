---
title: 解决 VMware Workstation 无法安装 tools
tags: [VMware,tools]
---

环境概要

|item|content|
|---|---|
|host OS|ubuntu 18.10|
|vm|VMware workstation|
|guest OS|windows 10 pro|


最近想要研究下 Adobe XD，学习怎么制作原型图。所以在虚拟机中安装了 win10。在安装 VMware tools 的时候，总是卡在下载完成后的安装步骤。VMware 的提示信息也不友好，通过查看日志得：

```
cat /var/log/vmware-installer


Traceback (most recent call last):
  File "/usr/lib/vmware-installer/2.1.0/vmware-installer.py", line 293, in main
    ui.Initialize(options.ui)
  File "/usr/lib/vmware-installer/2.1.0/vmis/ui/__init__.py", line 77, in Initialize
    exec 'from vmis.ui.null import *' in globals()
  File "<string>", line 1, in <module>
  File "/usr/lib/vmware-installer/2.1.0/vmis/ui/null.py", line 13, in <module>
    from vmis.ui import console
  File "/usr/lib/vmware-installer/2.1.0/vmis/ui/console.py", line 9, in <module>
    import curses
  File "/usr/lib/vmware-installer/2.1.0/python/lib/curses/__init__.py", line 15, in <module>
    from _curses import *
ImportError: libncursesw.so.5: cannot open shared object file: No such file or directory

```

从日志来看是缺少了库文件，但系统中只有 libncursesw.so.6 解决方法就是建立软连接

```
ln -s /lib/x86_64-linux-gnu/libncursesw.so.6 /lib/x86_64-linux-gnu/libncursesw.so.5
```

问题解决，特此记录
