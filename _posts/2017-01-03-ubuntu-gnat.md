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

首先，从 [GNAT 的官方网站](http://libre.adacore.com/) 上下载 GNAT 的 GPL 版。GNAT 作为 Ada 编程语言的“御用”开发环境，分为商业版和 GPL 版，其中 GPL 版是专供学术研究和个人使用的免费版本。

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
