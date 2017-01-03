---
layout: post
title:  "在 Ubuntu 上安装 Ada 开发环境：GNAT GPL 2016"
categories: Ada
tags:  Ada GNAT GPL
author: 辛亚平
---

* content
{:toc}

GNAT 是 Ada 编程语言的推荐编译器。本文介绍了如何在 Ubuntu 上安装 GNAT GPL 2016。

![](/attachment/daily/2017/0103/GPS.png)




## 软件环境

OS：Ubuntu 16.04.1 LTS (Xenial Xerus)

SW：GNAT GPL 2016

## 安装过程

首先，从 [GNAT 的官方网站](http://libre.adacore.com/) 下载 GNAT 的 GPL 版。GNAT 作为 Ada 编程语言的“御用”集成开发环境，分为商业版和 GPL 版，其中 GPL 版是专供学术研究和个人使用的免费版本。

我的机器是 64 位的，我下载的安装包是：gnat-gpl-2016-x86_64-linux-bin.tar.gz

安装过程：

```
mkdir Ada-gnat-2016
mv gnat-gpl-2016-x86_64-linux-bin.tar.gz Ada-gnat-2016/
cd Ada-gnat-2016
tar xvf gnat-gpl-2016-x86_64-linux-bin.tar.gz
cd gnat-gpl-2016-x86_64-linux-bin

sudo ./doinstall
```

安装界面虽然是纯文字的，但是整个过程非常清晰：

![](/attachment/daily/2017/0103/GNAT/A01-01.png)

![](/attachment/daily/2017/0103/GNAT/A01-02.png)

![](/attachment/daily/2017/0103/GNAT/A01-03.png)

![](/attachment/daily/2017/0103/GNAT/A01-04.png)

![](/attachment/daily/2017/0103/GNAT/A01-05.png)

这样我们的软件安装就完成了，但是现在还不能愉快地使用，所以我们现在要进入下一步骤：

## 环境变量设置

此时，如果我们执行：

```
gnatmake --version
```

我们会发现现在 gnatmake 是找不到的：

```
The program 'gnatmake' can be found in the following packages:
 * gnat-4.9
 * gnat-5
Try: sudo apt install <selected package>
```

怎样让系统能够找到我们刚刚安装的 GNAT 呢？执行下面的步骤：

```
sudo touch /etc/profile.d/gnat.sh
```

这样我们就创建了一个新文件：/etc/profile.d/gnat.sh

然后我们用文本编辑器编辑这个文件，比如：

```
sudo vi /etc/profile.d/gnat.sh
```

我们在这个文件里面增加一行内容：

```
export PATH=/usr/gnat/bin:$PATH
```

不想重起系统的话就执行下面的命令，令我们的环境变量设置生效：

```
source /etc/profile.d/gnat.sh
```

这个时候我们再执行：

```
gnatmake --version
```

会看到，系统能找到我们刚刚安装的 GNAT 了：

```
GNATMAKE GPL 2016 (20160515-49)
Copyright (C) 1992-2016, Free Software Foundation, Inc.
try "gnatmake --help" for more information.
```

## 运行 GNAT Ada IDE

在命令行中执行命令：

```
gps
```

就能看到 GNAT 启动起来了：

![](/attachment/daily/2017/0103/GNAT/A03-01.png)

![](/attachment/daily/2017/0103/GNAT/A03-02.png)
