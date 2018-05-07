---
layout: post
title:  "如何在 Ubuntu 上安装 Visual Studio Code"
categories: Tools
tags:  Ubuntu Linux Visual_Studio_Code
author: 辛亚平
---

* content
{:toc}

Visual Studio Code 是一个非常优秀的免费、跨平台且开源的代码编辑器，是微软贡献给开源社区的“良心之作”。

![Visual Studio Code running on Ubuntu Linux](/attachment/daily/2017/0804/vscode-on-ubuntu.png)

下面详细介绍在 Ubuntu Linux 上安装 Visual Studio Code 的过程。



## 安装

我们使用 umake 来安装 Visual Studio Code。先要保证 umake 已被正确安装。命令如下：

```
sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
sudo apt-get update
sudo apt-get install ubuntu-make
```

然后我们就可以用 umake 来安装 Visual Studio Code 了。命令如下：

```
umake ide visual-studio-code
```

上述命令中，我们给 Visual Studio Code 选择了一个程序组：“ide”。注意这个程序组的名称是大小写敏感的。在以下屏幕截图中，我故意在第一次的时候输错程序组名称，这样的话命令会执行失败，但是在返回的操作提示中会提示你应该选择哪些程序组。

![Install Visual Studio Code using umake: step 1](/attachment/daily/2017/0804/umake-install-vscode-step_1.png)

然后如以下屏幕截图所示，当提示是否选择接受软件许可时，当然选择“接受”（Accept）。

![Install Visual Studio Code using umake: step 1](/attachment/daily/2017/0804/umake-install-vscode-step_2.png)

接下来 unmake 会自动下载最新的 Visual Studio Code 并进行安装。不需要做任何操作干预，看着就好了。如图所示：

![Install Visual Studio Code using umake: step 1](/attachment/daily/2017/0804/umake-install-vscode-step_3.png)

## 卸载

卸载只需执行这条命令：

```
umake ide visual-studio-code --remove
```



## 参考文章

- [How To Install Visual Studio Code On Ubuntu](https://itsfoss.com/install-visual-studio-code-ubuntu/)

