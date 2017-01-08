---
layout: post
title:  "How to generate makefile from Code::Blocks project"
categories: C/C++
tags:  codeblocks makefile C C++
author: 辛亚平
---

* content
{:toc}

[Code::Blocks (codeblocks)](http://www.codeblocks.org/) 是一个跨平台的 C/C++ IDE，在 Linux 平台上我非常喜欢用它。但是，如果我希望和其他人共享我的代码，或者在其它环境中编译我的代码，这时候我就希望能够把 Code::Blocks 的工程文件导出为 makefile 文件。毕竟不是所有的 Linux 主机上都安装了 Code::Blocks。

经查，想要把 Code::Blocks 的工程文件导出为 makefile 文件，有两个工具可以选用：

- [cbp2make：命令行工具](https://sourceforge.net/p/cbp2make/wiki/Home/)
- [cbmakegen: Code::Blocks 插件](http://developer.berlios.de/projects/cbmakegen/)

我尝试了 cbp2make，下面我把具体的过程记录下来。




## 软件环境

OS：Ubuntu 16.04.1 LTS (Xenial Xerus)

SW：GNAT GPL 2016

## 准备

从 [cbp2make：命令行工具](https://sourceforge.net/p/cbp2make/wiki/Home/) 的官方网站上下载源代码。

现在下载到的源代码压缩包是：cbp2make-stl-rev147-all.tar.7z

后缀为 .tar.7z 的压缩包在 Linux 平台上不是很常见，解压它需要用到一个在 Windows 平台上耳熟能详的压缩/解压工具：7-zip。这个工具已经被移植到了 Linux 平台，叫做：p7zip。

安装命令：

```
sudo apt install p7zip
```

或者：

```
sudo apt install p7zip-full
```

解压 cbp2make-stl-rev147-all.tar.7z 之后，可以看到压缩包里面原来是一个 Code::Blocks 工程文件。编译它就能够得到 cbp2make。

## 使用

假设我有一个 Code::Blocks 工程文件叫做 fork-test.cbp，那么我们执行一下命令：

```
cbp2make -in fork-test.cbp -out makefile
```

就能看到 makefile 文件被自动生成了。

## 参考文章

- [Code::Blocks and Makefiles](http://wiki.codeblocks.org/index.php?title=Code::Blocks_and_Makefiles)
- [Code::Blocks Wiki: Tools+ reference](http://wiki.codeblocks.org/index.php/Tools%2B_reference#Export_makefile)
- [Code::Blocks导出MakeFile文件工具](https://my.oschina.net/qihh/blog/84650)
- [Topic: cbp2make - makefile generation tool](http://forums.codeblocks.org/index.php/topic,13675.0.html)
- [采用cbp2make工具由code::blocks工程创建makefile文件](http://blog.csdn.net/nick_wong/article/details/7718773)
- [code block自动生成makefile](http://www.cnblogs.com/vincenzo/archive/2011/08/22/2148955.html)
- [cbMakefileGen](https://sourceforge.net/projects/cbmakegen.berlios/)
- [利用cbmakegen导出Code::blocks的Makefile](http://blog.csdn.net/odaynot/article/details/8148905)






