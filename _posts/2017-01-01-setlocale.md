---
layout: post
title:  "如何在控制台中用 printf 正确地输出中文"
categories: Win32
tags:  VC++ Windows Win32
author: 辛亚平
---

* content
{:toc}

本文介绍了在 Win32 Console 环境中输出中文的小技巧。




## 问题

当我们帮家里的小弟弟小妹妹做 C 语言作业的时候，经常需要在控制台中输出中文。但是，如何正确地输出中文呢？并不是每个人都能一次就做成功哟。

## 解决办法

要想让控制台输出中文，首先必须保证 Windows 系统的 System Locale 被设置为中文：

![](/attachment/daily/2017/0101/system-locale-chs.png)

然后，代码中，在控制台输出之前，要有这样一句：

```c
setlocale(LC_CTYPE, "zh-CN");
```

printf() 输出中文的地方，要用 %ls 。例如：

```c
printf("%s %ls\n", ctxt, wtxt);
```

看一个完整的代码：

```c
#include "stdafx.h"
#include <locale.h>

int main()
{
    const char ctxt[] = "Display:";
    const wchar_t wtxt[] = L"简体中文的世界。";
    
    setlocale(LC_CTYPE, "zh-CN");
    printf("%s %ls\n", ctxt, wtxt);
    
    return 0;
}
```

编译运行一下，看看是不是完美地输出了中文字符串？

## 一个好玩的例子

在微博上面看到一个好玩的程序，我把菜单输出的代码写了出来：

```c
#include "stdafx.h"
#include <locale.h>

static int DisplayMenu();

int main()
{
    DisplayMenu();
    return 0;
}

static int DisplayMenu()
{
    const wchar_t* wtxts[] =
    {
        L"*****************************************",
        L"******** 欢迎我家小森森进入游戏！********",
        L"****     1. 这是什么游戏？怎么玩？   ****",
        L"****     2. 看完说明了，我要玩！     ****",
        L"****     3. 我要退出                 ****",
        L"**** I love you, love you, love you! ****",
        L"*****************************************",
        L"小森森，请选择："
    };
    
    unsigned char count = sizeof(wtxts) / sizeof(wchar_t*);
    unsigned char index = 0;
    int select = 0;
    
    setlocale(LC_CTYPE, "zh-CN");
    
    for (index = 0; index < count; index++}
    {
        printf("%ls", wtxts[index]);
        
        if (count - index > 1)
        {
            printf("\n");
        }
    }
    
    select = getchar();
    return select;
}
```

输出：

![](/attachment/daily/2017/0101/printf-chs.png)

## 进一步了解

看看下面这些文档：

- [MSDN: setlocale, _wsetlocale](https://msdn.microsoft.com/en-us/library/x99tb11d.aspx)
- [MSDN: Locale](https://msdn.microsoft.com/en-us/library/wyzd2bce.aspx)
- [C标准库的setlocale()用法笔记](http://www.cnblogs.com/hnrainll/archive/2011/05/07/2039700.html)
- [IBM Knowledge Center: setlocale() — Set locale](https://www.ibm.com/support/knowledgecenter/SSLTBW_1.13.0/com.ibm.zos.r13.bpxbd00/setloc.htm)
