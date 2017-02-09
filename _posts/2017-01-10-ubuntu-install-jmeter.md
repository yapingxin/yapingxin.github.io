---
layout: post
title:  "How to install Latest JMeter on Ubuntu"
categories: Tools
tags:  JMeter
author: 辛亚平
---

* content
{:toc}

这篇文章记录了在 Ubuntu 上安装 Apache JMeter 的步骤。



## 安装 Java 运行环境

Apache JMeter 是基于 Java 开发的免费开源 Web 性能测试软件。JMeter 3.x 要求的 Java 运行环境是 Java 7 或者更高的版本。

关于如何安装 Java 运行环境，可以参考之前写的小文：[《How to install specific version of Java on Ubuntu with apt-get》](https://yapingxin.github.io/2016/12/27/ubuntu-install-java/)


## 下载 JMeter

在 [Apache JMeter 的官方网站](http://jmeter.apache.org/index.html) 上，可以得到 JMeter 的最新稳定二进制版本：
[apache-jmeter-3.1.tgz](http://www.trieuvan.com/apache//jmeter/binaries/apache-jmeter-3.1.tgz)

```shell
mkdir ~/Public/Tools
cd ~/Public/Tools
wget wget http://www.trieuvan.com/apache//jmeter/binaries/apache-jmeter-3.1.tgz
tar -xf apache-jmeter-3.1.tgz
cd apache-jmeter-3.1/
```
## 执行 JMeter

执行以下命令：

```shell
./jmeter
```

就能看到 Apache JMeter 的界面启动起来了。


## 参考文章

- [stackoverflow: How to install latest jmeter in Ubuntu 15.10](http://stackoverflow.com/questions/37333339/how-to-install-latest-jmeter-in-ubuntu-15-10)
- [开源性能测试工具 > JMeter](http://www.ltesting.net/ceshi/open/kyxncsgj/jmeter/)
- [JMeter 使用入门](http://www.ltesting.net/ceshi/open/kyxncsgj/jmeter/2012/0801/205347.html)
- [jmeter入门教程- Jmeter教程及技巧汇总](http://www.hissummer.com/jmeter-summary.html)
