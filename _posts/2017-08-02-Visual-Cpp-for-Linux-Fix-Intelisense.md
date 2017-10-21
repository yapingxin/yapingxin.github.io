---
layout: post
title:  "修复 Visual C++ for Linux 的代码智能提示（Intelisense）功能"
categories: Tools
tags:  Visual_C++_for_Linux
author: 辛亚平
---

* content
{:toc}

针对 Visual C++ for Linux 这个插件：修复它的代码智能提示（Intelisense）功能。

![Visual C++ for Linux Development](/attachment/MSProd/MS_VCLinux_Logo_RU.jpg)



## 问题

自从 Visual Studio 2015 开始起，Visual C++ 开始能够进行 Linux 平台上的跨平台开发了，这个新特性十分振奋人心呢。其实就是安装一个 Visual C++ for Linux 的插件，安装了这个插件之后，Visual C++ 就能通过 SSH 把源代码部署到远程的 Linux 主机上，远程编译，并通过 gdbserver 远程调试。这个功能十分实用。

然而，在 Visual C++ (Windows) 这一端，写 Linux C/C++ 程序的时候，在 IDE 中会提示有一些头文件找不到，包括一些定义找不到，直接导致代码智能提示（Intelisense）失效。

比如下面这张截图：

![](/attachment/daily/2017/0111/Visual-Cpp-Linux-01.png)


其实呢，这些头文件可能在 Linux 主机上很正常地存在着。

比如我们现在就在 Linux 主机上找一下上图中的 unistd.h 文件：

![](/attachment/daily/2017/0111/Visual-Cpp-Linux-02.png)

可见这个文件是正常存在的。

这个问题倒也不影响编译，因为最终编译源代码的时候实际上是把源代码全部复制到 Linux 主机上，并在 Linux 主机上进行编译的。但是 IDE 的作用就是要让写代码的过程也智能起来，没有 Intelisense 功能，丧失了使用 IDE 的一大优势呢。

本文探讨了这个问题的解决办法。


## 分析

Visual C++ for Linux 是怎么样来找 Linux 上的头文件从而做到代码智能提示（Intelisense）的呢？实际上在创建 Linux 工程的时候它会从下面这些路径寻找预先存放好的 Linux 头文件：

```
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\include\c++\5
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\include\x86_64-linux-gnu\c++\5
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\include\c++\5\backward
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\lib\gcc\x86_64-linux-gnu\5\include
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\local\include
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\lib\gcc\x86_64-linux-gnu\5\include-fixed
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\include\x86_64-linux-gnu
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\\usr\include
```

上述文件夹我不确定是否会有所变动，其实你可以查看你自己的环境。

但是呢，当我们通过 Visual C++ for Linux 的 SSH 连接到 Linux 主机上以后，它并没有和 Linux 主机上的头文件保持同步。而且初始情况下它缺的头文件还是挺多的，这样就导致了 IDE 认为一些头文件找不到，导致代码智能提示（Intelisense）失效。


## 解决

为了解决这个问题，我通过 WinSCP 把远程 Linux 主机上的头文件下载下来。其实就是把 Linux 主机上的 /usr/include 文件夹整个下载下来。然后针对 C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include 缺失的头文件，缺什么补什么。

我是在写一个 socket 程序，对于缺失的头文件我曾经尝试补过这些头文件：

以 src 代表源文件夹，dst 代表目的文件夹。

src[1]: /usr/include

dst[1]: C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\usr\include

拷贝了这些文件和文件夹：

netinet/*.*

arpa/*.*

asm-generic/*.*

linux/*.*

src[2]: /usr/include/x86_64-linux-gnu

dst[2]: C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\Linux\include\usr\include\x86_64-linux-gnu

拷贝了所有的文件和文件夹：

这才让 socket 编程所涉及到的那些个头文件能正常找到。

其实我也是死心眼，直接把 src[1] 下面的所有文件和文件夹，覆盖到 dst[1]，就解决了。如果不放心的话覆盖之前做好备份工作就行了。

你看下面这幅截图，所有的头文件都不再提示找不到了：

![](/attachment/daily/2017/0111/Visual-Cpp-Linux-03.png)


## 参考文章

- [Visual C++ for Linux Development](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/#includes)
- [Microsoft/VSLinux: Issues](https://github.com/microsoft/vslinux/issues?page=2&q=is%3Aissue+is%3Aopen)
- [Issues: Improve Intelisense support #37](https://github.com/Microsoft/VSLinux/issues/37)
- [Issues: Source dependencies on header files are not correctly applied to incremental build #29](https://github.com/Microsoft/VSLinux/issues/29)
- [Issues: Automatically sync include files from Linux #43](https://github.com/Microsoft/VSLinux/issues/43)


