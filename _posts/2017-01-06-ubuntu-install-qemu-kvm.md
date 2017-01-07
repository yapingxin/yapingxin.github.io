---
layout: post
title:  "在 Ubuntu 上安装 QEMU、KVM"
categories: QEMU
tags:  Ubuntu QEMU KVM
author: 辛亚平
---

* content
{:toc}

本文介绍了如何在 Ubuntu 上安装 QEMU、KVM。




## 软件环境

OS：Ubuntu 16.04.1 LTS (Xenial Xerus)

SW：GNAT GPL 2016

## 准备

由于 KVM 必须在支持硬件虚拟化的机器上运行，所以我们要检查一下自己的 CPU 是否支持硬件虚拟化。无论 Intel VT-x 还是 AMD-V 都是可以的。检查的办法就是执行下面的语句：

```
egrep -c '(svm|vmx)' /proc/cpuinfo
```

如果输出结果为 0 那么说明不支持硬件虚拟化，其它的输出结果都是表明支持硬件虚拟化。比如说我在 Dell E6410 笔记本上执行的结果是：

```
4
```

## 安装 QEMU、KVM

```
sudo apt-get install qemu
sudo apt-get install qemu-kvm libvirt-bin bridge-utils virt-manager
```

## 权限设置

只有 root 和 libvirtd 组里面的用户才有权限创建 KVM 虚拟机。所以现在我们要把我们自己的用户名加入到 libvirtd 组。具体的命令是：

```
sudo adduser <username> libvirtd
```

注意要把上述命令的 <username> 替换成你自己的用户名。比如我自己执行的命令：

```
sudo adduser yaping libvirtd
```

## 开始使用

现在重新登录系统或者重启。然后，执行下列命令查看虚拟机列表：

```
sudo virsh -c qemu:///system list
```

现在我们看到的是一个空列表，执行结果如下：

```
 Id    Name                           State
----------------------------------------------------

```

虽然看到的是个空列表，但是如果能看到这个输出结果，至少说明安装成功，一切以经准备就绪了。

## 参考文章

- [How to Install KVM and Create Virtual Machines on Ubuntu](http://www.howtogeek.com/117635/how-to-install-kvm-and-create-virtual-machines-on-ubuntu/)
- [qemu的安装步骤详解(适合ubuntu和windows)](http://blog.csdn.net/ustc_dylan/article/details/4178381)




