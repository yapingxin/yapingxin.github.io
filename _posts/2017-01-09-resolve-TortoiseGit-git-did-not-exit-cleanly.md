---
layout: post
title:  "How to resolve “git did not exit cleanly (exit code 1)” error on TortoiseGit?"
categories: Git
tags:  TortoiseGit Git
author: 辛亚平
---

* content
{:toc}

这篇文章记录了解决 “git did not exit cleanly (exit code 1)” 错误的方法。



## 问题

当我试图用 TortoiseGit commit & push 我的代码的时候，出现以下错误：

```shell
git.exe pull --progress -v --no-rebase "origin"

fatal: unable to access 'https://github.com/yapingxin/yapingxin.github.io.git/': Unknown SSL protocol error in connection to github.com:443


git did not exit cleanly (exit code 1) (1310 ms @ 2/9/2017 7:49:33 PM)
```

![](/attachment/daily/2017/0109/git-not-exit-cleanly.png)


## 分析

为了获得更详细的信息，我在 Git Bash 中执行了 git push 命令，看到了不一样的报错信息：

```shell
PACRIM1+e547156@CH5OLT2Q5R562 MINGW64 /c/GIT/github/yapingxin.github.io (master)
$ git push
fatal: unable to access 'https://github.com/yapingxin/yapingxin.github.io.git/': Unknown SSL protocol error in connection to github.com:443

```

![](/attachment/daily/2017/0109/git-SSL-error.png)

与此同时我广泛地 Google，看到在 [stackoverflow](http://stackoverflow.com/questions/9617336/how-to-resolve-git-did-not-exit-cleanly-exit-code-128-error-on-tortoisegit) 上面有人说这个问题可能是因为 SSH Key 出了问题，重新生成一个新的即可。

原文：

> It's probably because your SSH key has been compromised. Make a new one and add it to your GitHub account.

## 解决方法

我仅仅是重新用 git config 设置了一下用户信息，git 就恢复正常了：

```shell
git config --global user.email "xinyp@live.com"
git config --global user.name "Yaping Xin"
```

然后就能正常 push 了：

![](/attachment/daily/2017/0109/git-OK.png)

接下来再用 TortoiseGit 操作，也正常了。


## 参考文章

- [stackoverflow: How to resolve “git did not exit cleanly (exit code 128)” error on TortoiseGit?](http://stackoverflow.com/questions/9617336/how-to-resolve-git-did-not-exit-cleanly-exit-code-128-error-on-tortoisegit)

