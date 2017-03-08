---
layout: post
title:  "创建 / 自定义 Visual Studio 2017 的离线安装包"
categories: Tools
tags:  Visual_Studio
author: 辛亚平
---

* content
{:toc}

就在昨天半夜的时候（北京时间），Visual Studio 2017 的正式版如约发布了，这是微软技术圈里的一件大事，我当然也第一时间进行了体验。

这篇短文介绍了如何创建自己的 Visual Studio 2017 离线安装包，希望对您有所帮助。



## 问题

从 [官方](www.visualstudio.com) 下载的 Visual Studio 2017 安装文件依然继承了上一个版本的特点，只有 1,014 KB，很显然这是一个 Web 安装文件，它在安装的过程中才现去微软的网站上下载相关的组件的安装包。

这就给像我这样的工程师出了一个难题，因为我并不能保证网络链接始终是稳定可靠的，万一安装的过程中下载不畅，还要在重来，岂不浪费了时间。

所以创建一个离线安装包是十分有必要的。

## 创建离线安装包的命令

好在微软的官方文档提到了如何创建离线安装包。文章如下：

- [Create an offline installer for Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/install/create-an-offline-installation-of-visual-studio)

我下载的是社区版（Community Edition），下载下来的安装文件是：vs\_community__186468815.1477979930.exe


根据文档，把该文件重命名为：vs\_community.exe

然后，假如我需要把离线安装包创建在这里：C:\Pub\Tools\Microsoft\vs2017offline

那么我需要在命令行中执行：
```
vs_community.exe --layout C:\Pub\Tools\Microsoft\vs2017offline
```

如果我们创建一个包含所有功能、所有语言的离线安装包，听说那个包会非常大，有好几十 G 吧。我网速又不高，这要下载到什么时候去呢？

所以为了只包含我们需要的部分，创建一个小一点的离线安装包，就需要在创建离线安装包的时候加一些参数。

根据文档，我们可以加上以下几个参数来缩小安装包的体积：

--lang en-US

这个参数是为了只包含英文安装文件。工程师应该都比较习惯英文版的 Visual Studio 吧，所以我们就不下载那些中文、法文、日文之类的文件了。。。


--add <workload\>

上面的 <workload\> 就是具体你要安装哪些功能。Visual Studio 2017 是一个非常庞大的工具，但有很多功能你不一定用得上，那些用不上的部分就不要下载更不要安装了。

workload 这个词以前没有出现过，它是什么意思呢？请看以下截图，这是正常安装 Visual Studio 2017 的时候需要选择安装的组件：

![](/attachment/daily/2017/0308/VS2017-Install-A01.png)

你在这个界面中选择的组件，就是 workload。

在微软官方文档中详细给出了workload 的列表：

- [Visual Studio Community 2017 workload and component IDs](https://docs.microsoft.com/en-us/visualstudio/install/workload-component-id-vs-community)

作为一个 C++ 开发者，偶尔我会写写 C#，所以我选择的安装组件是：

1. Visual Studio core editor (included with Visual Studio Community 2017)
2. Linux development with C++
3. Desktop development with C++
4. Universal Windows Platform development

所以我选择的 workload 是：

1. Microsoft.VisualStudio.Workload.CoreEditor
2. Microsoft.VisualStudio.Workload.NativeCrossPlat
3. Microsoft.VisualStudio.Workload.NativeDesktop
4. Microsoft.VisualStudio.Workload.Universal


所以，我最终的创建离线安装包的命令是：

```
vs_community.exe 
  --layout C:\Pub\Tools\Microsoft\vs2017offline 
  --lang en-US 
  --add 
        Microsoft.VisualStudio.Workload.CoreEditor 
Microsoft.VisualStudio.Workload.NativeCrossPlat 
Microsoft.VisualStudio.Workload.NativeDesktop 
Microsoft.VisualStudio.Workload.Universal

```

注意以上命令为了好看我特意进行了一点排版，实际上参数之间用空格分开就可以了。也就是说，我实际上执行的命令是：

```
vs_community.exe --layout C:\Pub\Tools\Microsoft\vs2017offline --lang en-US --add Microsoft.VisualStudio.Workload.CoreEditor Microsoft.VisualStudio.Workload.NativeCrossPlat Microsoft.VisualStudio.Workload.NativeDesktop Microsoft.VisualStudio.Workload.Universal
```

## 创建离线安装包的运行过程

以上命令在命令行中执行，以下是执行过程中的截图：

![](/attachment/daily/2017/0308/VS2017-Create-Offline-Package-A01.png)

![](/attachment/daily/2017/0308/VS2017-Create-Offline-Package-A02.png)

进过大约两个小时的时间，下载完毕，最终得到的安装包的大小是：2.07 GB

这个大小已经相当可以了。

![](/attachment/daily/2017/0308/VS2017-Create-Offline-Package-A03.png)

然后用离线安装包安装：

![](/attachment/daily/2017/0308/VS2017-Install-A01.png)

![](/attachment/daily/2017/0308/VS2017-Install-A02.png)

![](/attachment/daily/2017/0308/VS2017-Install-A03.png)




## 参考文章

- [Create an offline installer for Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/install/create-an-offline-installation-of-visual-studio)
- [Visual Studio Community 2017 workload and component IDs](https://docs.microsoft.com/en-us/visualstudio/install/workload-component-id-vs-community)
- [Visual Studio administrator guide for Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/install/visual-studio-administrator-guide)
- [Visual Studio Settings](https://msdn.microsoft.com/en-us/library/2ewd52wf(v=vs.100).aspx)


