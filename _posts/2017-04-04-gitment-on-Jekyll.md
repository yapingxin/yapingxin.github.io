---
layout: post
title:  "为 Jekyll 博客添加 gitment 评论系统"
categories: Jekyll
tags:  Jekyll gitment
author: 辛亚平
---

* content
{:toc}

本文介绍了为 Jekyll 博客添加 gitment 评论系统的注意事项。



## 注意事项

为 Jekyll 博客添加 gitment 评论系统，如何去做，这篇文章说得非常清楚了：《[为 Jekyll 博客添加 gitment 评论系统](http://www.cnblogs.com/jacobpan/p/7200512.html)》

我想说的两点注意事项：

1. Authorization callback URL 就是自己的 Jekyll 博客的地址。比如说本博客的此项设置就是：https://yapingxin.github.io/

2. 在 post.html 中添加的 html 和 javascript 代码中，repo 就是博客的 repository 的名字，而不是 repository 的地址。比如说本博客的 repo 就是：yapingxin.github.io




## 参考文章

- [在Jekyll博客添加评论系统：gitment篇](http://www.cnblogs.com/jacobpan/p/7200512.html)
- [Gitment：使用 GitHub Issues 搭建评论系统](https://segmentfault.com/p/1210000009867081/read)
- [为 hexo NexT 添加 Gitment 评论插件](https://meesong.github.io/StaticBlog/2017/NexT+Gitment/)
- [体验GitHub Issues的评论系统——Gitment](https://www.tiexo.cn/gitment/)
- [Gitment：使用 GitHub Issues 搭建评论系统](https://juejin.im/entry/591118a5a22b9d00580d0fcb)

