---
title: 技巧：在Bash中增加环境变量
tags: [Bash]
grammar_cjkRuby: true
---

通常情况下，安装程序后要配置环境变量，例如 JDK 安装在 /opt/jdk 则需要如下环境变量配置：

```
vim ~/.profile

# append JDK variable and save file
export JAVA_HOME=/opt/jdk
export PATH=$JAVA_HOME/lib:\$PATH

# resource profile
source ~/.profile
```

通过在 ~/.bashrc 中增加工具方法，可以大大简化环境变量的配置过程。

```
# 在 ~/.bashrc 中增加以下方法并保存
prepend() { [ -d "$2" ] && eval $1=\"$2':'\$$1\" && export $1; }
# resource bashrc
source ~/.bashrc
```

在完成上述改造后，配置 JDK 环境变量的过程可简化为：

```
prepend PATH /opt/jdk/bin
```
