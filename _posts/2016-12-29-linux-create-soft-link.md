---
layout: post
title:  "Linux Tips: 创建应用程序的软链接"
categories: Linux
tags:  Linux
author: 辛亚平
---

* content
{:toc}

本文介绍了在 Linux 环境下创建软链接的命令：ln -s




## 软链接

当我们在 Linux 上安装了 Eclipse 之后，每次总要输入完整的路径才能启动 Eclipse：

```
/usr/local/eclipse/eclipse
```

如果能够给 Eclipse 创建一个快捷方式就好了！办法当然是有的，那就是：给 Eclipse 程序创建一个软链接。

相应的命令：

```
sudo ln -s /usr/local/eclipse/eclipse /etc/eclipse
```

然后，在 /etc/environment 这个文件里面，修改环境变量 PATH，在 PATH 的路径中增加 /etc：

```
sudo nano /etc/environment
```

每个人的 /etc/environment 可能都是不一样的，我的 /etc/environment 文件的内容如下（修改后）：

```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/etc"
JAVA_HOME="/usr/lib/jvm/java-8-oracle"
```

然后为了使这个修改不需要重启立即生效，执行：

```
source /etc/environment
```

这样做以后，当我们再次需要启动 Eclipse 的时候，就不需要敲那么老长的路径名了，直接敲下面这个命令就好了：

```
eclipse
```

## 解释：ln 命令

ln 命令可以为文件或者目录创建链接。如果不加 -s 命令，则创建的使硬链接，加了 -s 参数则创建的是软链接。硬链接是一个与源文件一样大小的文件，而软链接则是像 Windows 系统下的快捷方式。无论硬链接还是软链接，当源文件发生变化时，链接都会与之保持同步。

对于 ln 命令更详细的解释，还是查询专门的文档或者敲 man ln 吧。


