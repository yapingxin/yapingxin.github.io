---
layout: post
title:  "How to install specific version of Java on Ubuntu with apt-get"
categories: Ubuntu
tags:  Ubuntu Java
author: 辛亚平
---

* content
{:toc}

在这篇教程中，我将演示如何在 Ubuntu Linux 发行版本上通过 apt-get 安装特定版本的 Java。




## 软件环境

OS：Ubuntu 16.04.1 LTS (Xenial Xerus)

SW：现在是 2016 年 12 月 27 日，当前 Java 最新的稳定版本为：Java 8 Update 111（October 18, 2016）

## 查看已安装的 Java 的版本 / 判断是否已经安装 Java

通过以下命令可以查看当前安装的 Java 版本：

```
java -version
```

在我们演示用的计算机上，以上命令的输出为：

```
The program 'java' can be found in the following packages:
 * default-jre
 * gcj-5-jre-headless
 * openjdk-8-jre-headless
 * gcj-4.8-jre-headless
 * gcj-4.9-jre-headless
 * openjdk-9-jre-headless
Try: sudo apt install <selected package>
```

这段消息的意思其实就是说没找到，说明我们还没有安装 Java。

## 安装默认版本的 JRE / JDK

命令如下：

```
sudo apt-get update
sudo apt-get install default-jre default-jdk
```

装好了。看看已安装的版本是啥：

```
java -version
```

输出：

```
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-8u111-b14-2ubuntu0.16.04.2-b14)
OpenJDK 64-Bit Server VM (build 25.111-b14, mixed mode)
```

## 安装 Oracle JDK 8

有时候我们需要安装某个特定版本的 JRE / JDK，比如说 Oracle JDK 8。命令如下：

```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update

sudo apt-get install oracle-java8-installer
```

会弹出用户协议。点 OK / Yes。这里也没有别的选择，除非你想终止安装：

![](/attachment/daily/2016/1227/ubuntu-install-java-screenshots-s01-01-oracle-jdk.png)

![](/attachment/daily/2016/1227/ubuntu-install-java-screenshots-s01-02-oracle-jdk.png)

然后就开始下载、安装了。安装好之后会有下面的提示：

```
159744K ........ ........ ........ ........ ........ ........ 91%  155K 65s
162816K ........ ........ ........ ........ ........ ........ 93%  260K 51s
165888K ........ ........ ........ ........ ........ ........ 95%  292K 37s
168960K ........ ........ ........ ........ ........ ........ 97%  279K 23s
172032K ........ ........ ........ ........ ........ ........ 98%  299K 9s
175104K ........ ........ ........ ........                  100%  296K=13m10s

2016-12-28 01:50:12 (224 KB/s) - ‘jdk-8u111-linux-x64.tar.gz’ saved [181442359/181442359]

Download done.
Removing outdated cached downloads...
update-alternatives: using /usr/lib/jvm/java-8-oracle/jre/bin/ControlPanel to provide /usr/bin/ControlPanel (ControlPanel) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-oracle/jre/bin/javaws to provide /usr/bin/javaws (javaws) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-oracle/jre/bin/jcontrol to provide /usr/bin/jcontrol (jcontrol) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-oracle/bin/javafxpackager to provide /usr/bin/javafxpackager (javafxpackager) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-oracle/bin/javapackager to provide /usr/bin/javapackager (javapackager) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-oracle/bin/jmc to provide /usr/bin/jmc (jmc) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-oracle/bin/jvisualvm to provide /usr/bin/jvisualvm (jvisualvm) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-oracle/jre/lib/amd64/libnpjp2.so to provide /usr/lib/mozilla/plugins/libjavaplugin.so (mozil
la-javaplugin.so) in auto mode
Oracle JRE 8 browser plugin installed
Oracle JDK 8 installed

#####Important########
To set Oracle JDK8 as default, install the "oracle-java8-set-default" package.
E.g.: sudo apt install oracle-java8-set-default.
Setting up oracle-java8-set-default (8u111+8u111arm-1~webupd8~0) ...
```

如果以后就想使用 Oracle JDK 8 了，那么就按提示安装“oracle-java8-set-default”就好了。但是现在我还不想这么做，因为我们前面安装了 python-software-properties，所以我们任何时候都能够手动切换默认的 Java 版本。

顺便再执行一下 java -version 命令：

```
java -version
```

输出：

```
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)
```

## 设置默认的 Java 版本

当我们安装了多个 Java 版本的时候，可以通过 update-alternatives 来切换默认的 Java 版本。

命令如下：

```
sudo update-alternatives --config java
```

输出：

```
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
  0            /usr/lib/jvm/java-8-oracle/jre/bin/java          1081      auto mode
  1            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
* 2            /usr/lib/jvm/java-8-oracle/jre/bin/java          1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```

此时如果你想改变默认的 Java 版本的话，选择相应的数字即可。如果不想改变当前设置就直接按回车。

同理，执行：

```
sudo update-alternatives --config javac
```

输出：

```
There are 2 choices for the alternative javac (providing /usr/bin/javac).

  Selection    Path                                         Priority   Status
------------------------------------------------------------
  0            /usr/lib/jvm/java-8-oracle/bin/javac          1081      auto mode
  1            /usr/lib/jvm/java-8-openjdk-amd64/bin/javac   1081      manual mode
* 2            /usr/lib/jvm/java-8-oracle/bin/javac          1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```

不再赘述。

您还可以试着执行以下命令，同样也能切换相应的 Java 工具链（toolchain）：

```
sudo update-alternatives --config keytool
sudo update-alternatives --config javadoc
sudo update-alternatives --config jarsigner
```

## 设置默认的 Java 的环境变量 "JAVA_HOME"

要想使 Java 相关的软件正常运行，环境变量"JAVA_HOME"的设置是非常重要的。下面我们来设置它。

首先我们要知道正确的 Java Home 目录。我们是用 apt-get 来安装 Java 的，不像那种下载源代码来编译的安装方式，所以我们前面一直都没有在意 Java Home 目录，怎么办呢？

不要着急，其实前面我们执行“sudo update-alternatives --config java”命令的时候，已经可以从它的输出结果中知道 Java Home 目录了。

比如说，我们当时得到的 java 的目录是：

```
/usr/lib/jvm/java-8-oracle/jre/bin/java
```

再看看 javac 的目录：

```
/usr/lib/jvm/java-8-oracle/bin/javac
```

那么 Java Home 目录其实就是：

```
/usr/lib/jvm/java-8-oracle
```

还是很好得到的。

现在我们在 /etc/environment 中，增加一条这样的环境变量设置：

```
JAVA_HOME="YOUR_PATH"
```

具体在本例中，就是：

```
JAVA_HOME="/usr/lib/jvm/java-8-oracle"
```


执行：

```
sudo vi /etc/environment
```

![](/attachment/daily/2016/1227/ubuntu-install-java-screenshots-s02-01.png)

如果不想重启就想令刚才的环境变量"JAVA_HOME"设置生效，执行：

```
source /etc/environment
```

到底有没有生效呢？执行以下语句来检验一下：

```
echo $JAVA_HOME
```

输出：

```
/usr/lib/jvm/java-8-oracle
```

验证通过。

