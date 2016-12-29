---
layout: post
title:  "通过 SSH 与 Xming 执行远程 Linux 主机上的 GUI 应用程序"
categories: Linux
tags:  Linux SSH Xming
author: 辛亚平
---

* content
{:toc}

SSH 不仅可以远程执行 Linux 主机上的命令行程序，也可以执行带图形化界面的应用程序，使我们在本地看到 Linux 上的图形化界面。听上去很神奇吧。这是因为 Linux 的图形化界面是基于 X Window 的，X 的服务器与客户端可以分部在不同的主机上。如果我们在本地运行一个 X Server，然后以远程 Linux 为 X Client，这样我们就能在本地执行远程 Linux 主机上的图形化应用程序。




## 软件环境

远程 Linux 主机：
- OS：Linux + 桌面环境（例如：Ubuntu 16.04.1 LTS Xenial Xerus + gnome）
- OpenSSH Server

本地：
- OS：Windows
- Xming
- PuTTY

## 软件安装

### 远程 Linux 主机：安装 SSH Server

首先你要有一个安装了桌面环境的 Linux 主机。

在 Ubuntu 上我这样安装 gnome：

```
sudo apt install gnome-session-flashback
```

然后我们还需要安装 SSH Server。绝大对数的 Linux 主机上都装了，但是在这里我还是再啰嗦一下。

在 Red Hat、Fedora 或者 CentOS 这样的 Linux 发行版本是上，可以通过下面的命令安装 SSH Server：

```
sudo yum install openssh-server
```

在 Debian、Ubuntu 这样的 Linux 发行版本是上，可以通过下面的命令安装 SSH Server：

```
sudo apt-get install openssh-server
```

其它的 Linux 发行版本：请自行搜索。


### 本地 Windows 工作站：安装 PuTTY

去 PuTTY 的官方网站上面下载安装即可：[http://www.putty.org](http://www.putty.org)

### 本地 Windows 工作站：安装 X Server

其实 Windows 上面的 X Server 有很多选择，有一些是付费的。在这里我们选择的是开源且免费的 Xming。其官方网站为：
- [http://www.straightrunning.com/XmingNotes/](http://www.straightrunning.com/XmingNotes/)
- [https://sourceforge.net/projects/xming/](https://sourceforge.net/projects/xming/)

目前我们能免费下载到的 Xming 稳定版是：6.9.0.31。（最新版 7.7.0.13 需要在网站上捐钱之后才能获得下载账号）

安装过程毫无悬念：

![](/attachment/daily/2016/1228/Xming-01.png)

![](/attachment/daily/2016/1228/Xming-02.png)

![](/attachment/daily/2016/1228/Xming-03.png)

执行起来以后会最小化在 Windows 系统托盘里面：

![](/attachment/daily/2016/1228/Xming-04.png)


## 在 PuTTY 上的设置

启用 Connection \| SSH \| X11 \| Enable X11 forwarding 这个选项。

![](/attachment/daily/2016/1228/PuTTY-01.png)

![](/attachment/daily/2016/1228/PuTTY-02.png)

## 执行远程 Linux 主机上的 GUI 应用程序

终于到了可以看看效果的时候了。

假设我们已经在 Linux 主机上安装了 Codelite，这是一个著名的跨平台的 C/C++ IDE。如果没有安装它，你也可以尝试着启动 Linux 上的其它的带图形界面的应用程序，比如 Firefox 之类的。

![](/attachment/daily/2016/1228/Remote-01.png)

为了显摆一下我下面看到的界面是在 Windows 上显示出来的，我故意打开 VC++ 6.0 作为背景，呵呵。

![](/attachment/daily/2016/1228/Remote-02.png)

看上图。在 Windows 桌面上显示出来了一个明显是 Linux 风格的 CodeLite 界面。爽不爽？

这就是我今天要分享的 Linux 小技巧。:-)

## 后记

1. 关于 Xming 的详细的用法，请参考 [xmingrc](http://www.straightrunning.com/XmingNotes/xmingrc.php)，这是 Xming 的官方说明手册。可以看到 Xming 是一个极其强大的工具，还是有很多地方可以详细设置的。
2. 除了 Xming 之外，在 GitHub 上还活跃着另外一个开源且免费的 Windows 平台上的 X Server，它就是：[VcXsrv (Visual C++ X-server)](https://github.com/theqvd/vcxsrv)。从它的名字就可以猜到了，它是用 Visual C++ 开发的一个 X Server 程序。据说它比 Xming 还要好，而且状态比 Xming 更活跃。今天没空试试它了，改日再说吧。
