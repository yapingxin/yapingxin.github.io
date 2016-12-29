---
layout: post
title:  "Ubuntu 安装简体中文 Google 拼音输入法"
categories: Linux
tags:  Ubuntu 输入法 fcitx
author: 辛亚平
---

* content
{:toc}

在 Ubuntu 的桌面环境中安装中文输入法非常简单。在这篇教程中，我将演示如何在 Ubuntu 系统上安装基于 fcitx 框架的谷歌拼音输入法。

注：谷歌拼音输入法有基于 ibus 框架的，也有基于 fcitx 框架的。鉴于 ibus 框架的谷歌拼音输入法已经不更新了，我们就只介绍基于 fcitx 框架的。





## 软件环境

OS：Ubuntu 16.04.1 LTS (Xenial Xerus) + Gnome Desktop 界面显示语言：英文

SW：im-config，Google Pinyin (Fcitx)

## 安装/设置步骤

### 第 1 步：安装中文语言包

从 System Settings 中，选择：Language Support。点击：Install / Remove Languages... ，安装 Chinese (simplified)。

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s01-01.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s01-02.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s01-03.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s01-04.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s01-05.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s01-06.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s01-07.png)

### 第 2 步：安装输入法

执行以下命令：

```
sudo apt-get update
sudo apt-get install fcitx fcitx-googlepinyin im-config

im-config
```

在 im-config 界面中，将 fcitx 设为默认的输入法框架：

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s02-01.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s02-02.png)

然后重启系统。你会发现，桌面的右上角出现了 fcitx 的图标（就是那个小企鹅）。

### 第 3 步：设置输入法

从 System Settings 中，选择：Text Entry \| Input Sources，进入输入法设置（Input Method Configuration）。点左下角的“+”号，增加谷歌输入法:

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s03-01.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s03-02.png)

![](/attachment/daily/2016/1226/ubuntu-chinese-input-screenshots-s03-03.png)

你还可以继续设置切换输入法的热键，或者用默认的快捷键（<Ctrl> + <Space>）进行输入法切换。

安装和设置结束。
