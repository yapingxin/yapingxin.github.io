---
layout: post
title:  "��ŷ��ɸ��Ѱ����"
categories: Algorithm
tags:  Algorithm Prime Mathematics
author: ����ƽ
---

* content
{:toc}

��ŷ��ɸ��Ѱ������ C ���Ե����ӡ�



## ����

[code]

// Prime_EulerSelect.c : Defines the entry point for the console application.
//

#include "stdafx.h"

typedef unsigned __int8   uint8_t;
typedef unsigned __int16  uint16_t;
typedef unsigned __int32  uint32_t;

//#define Prime_Search_MAX 2000000

#define Prime_Search_MAX    334400
#define Prime_COUNT_MAX     (Prime_Search_MAX / 10)


int main()
{
    uint8_t selbuf[Prime_Search_MAX + 1];
    uint32_t prime[Prime_COUNT_MAX];

    uint32_t idx_select = 0;
    uint32_t idx_prime = 0;
    uint32_t count = 0;

    memset(selbuf, 0, (Prime_Search_MAX + 1) * sizeof(uint8_t));
    memset(prime, 0, Prime_COUNT_MAX * sizeof(uint32_t));

    for (idx_select = 2; idx_select <= Prime_Search_MAX; idx_select++)
    {
        if (selbuf[idx_select] == 0)
        {
            prime[count++] = idx_select;
        }

        for (idx_prime = 0; idx_prime < count && idx_select*prime[idx_prime] <= Prime_Search_MAX; idx_prime++)
        {
            selbuf[idx_select * prime[idx_prime]] = 1;

            if (idx_select % prime[idx_prime] == 0) break;
        }
    }

    for (idx_prime = 0; idx_prime < count; idx_prime++)
    {
        printf("%d ", prime[idx_prime]);
    }

    printf("\n\nPrime numbers count: %d\n", count);

    return 0;
}




[/code]


## �ο�����

- [ŷ��ɸ��������](http://www.cnblogs.com/A-S-KirigiriKyoko/p/6034584.html)
- [ŷ��ɸ��ʵ��������Ŀ���ɸȡ](http://www.itwendao.com/article/detail/390669.html)
- [����֮ �����ӷֽ⣬����ɸѡ����ŷ����������չŷ������㷨������](https://yq.aliyun.com/articles/15370)
- [Eratosthenesɸ����ŷ��ɸ���Ա�](http://www.xuebuyuan.com/1939896.html)



