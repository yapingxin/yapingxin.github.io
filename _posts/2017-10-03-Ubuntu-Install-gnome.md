---
layout: post
title:  "为 Ubuntu 安装 gnome 桌面"
categories: Linux
tags:  Ubuntu gnome Unity lightdm gdm
author: 辛亚平
---

* content
{:toc}

可能是因为我用的不是触摸屏电脑的缘故吧，对于 Ubuntu 的 Unity 桌面，一直不习惯，还是怀念以前经典的 gnome 桌面。

所以在本文中我们来介绍如果为 Ubuntu 安装 gnome 桌面，以及如何卸载 Ubuntu 自带的 Unity 桌面。



## 软件环境

我的 Ubuntu 版本是：Ubuntu 16.04.3 LTS (Xenial Xerus)

## 安装 gnome 桌面

只需一行命令即可搞定：

```
sudo apt-get install gnome-session-flashback
```

当然了，在执行这行命令之前，如果你先执行下面两行命令，那么我会认为你具有良好的 Ubuntu 使用习惯：

```
sudo apt-get update
sudo apt-get upgrade
```

安装完 gnome-session-flashback 这个包（以及它所依赖的包）之后，就可以重启 Ubuntu 了。重启之后，在登录界面上，就可以选择 gnome flashback 桌面来登录。只选一次就好了，以后登录的时候，Ubuntu 会记住你的这个选项。


## 卸载 Unity

现在你已经可以在 Ubuntu 上使用 gnome 桌面了，目的已经达到。但如果你介意 Unity 桌面依然占着你的硬盘，你可以卸载 Unity。

卸载的步骤如下：

（1）首先安装 gdm

```
sudo apt-get install gdm
```

然后，配置 X 的默认的界面管理器，将 Default Display Manager 设置为 gdm：

```
sudo dpkg-reconfigure lightdm
```

![](/attachment/daily/2017/1003/Uninstall-Unity/A02-01.png)

![将 Default Display Manager 设置为 gdm](/attachment/daily/2017/1003/Uninstall-Unity/A02-02.png)


接下来就可以卸载掉不再需要的软件包了：

```
sudo apt-get remove unity
sudo apt-get remove lightdm
sudo apt-get remove ubuntu-desktop
sudo apt-get remove --purge unity
sudo apt-get remove --purge lightdm
sudo apt-get autoremove
```


## 也可以不卸载 lightdm

其实我觉得 lightdm 比 gdm 好一些。你也可以不卸载 lightdm，依然使用 lightdm 为 Default Display Manager。

这样的话，就只需要卸载掉 unity 就可以了：

```
sudo apt-get remove unity
sudo apt-get remove --purge unity
sudo apt-get autoremove
```

## 注意事项

我发现，当 Default Display Manager 发生变化以后，输入法可能会需要重新配置一下。



## 参考文章

- [How can you remove Unity?](https://askubuntu.com/questions/6302/how-can-you-remove-unity)
- [Can I remove Unity now and how?](https://askubuntu.com/questions/651013/can-i-remove-unity-now-and-how)
- [How to Install the Gnome Classic Desktop in Ubuntu 14.04](https://www.howtogeek.com/189912/how-to-install-the-gnome-classic-desktop-in-ubuntu-14.04/)
- [Install Gnome Classic (Gnome Session Fallback) to Ubuntu 12.04](http://blog.csdn.net/shaonan155/article/details/17789619)


