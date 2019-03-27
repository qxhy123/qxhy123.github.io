---
layout: post
title: Linux内核学习阶段总结
author: "我不叫大脸猫"
header-style: text
tags:
    - linux kernel
    - 学习笔记
---


##  Linux内核学习阶段总结

前段时间为了深入探究Docker即Linux容器的底层实现原理，踏上了Linux内核学习这条不归路。
说是不归路并不是说Linux内核有多么佶屈聱牙，而是Linux实在太有意思了。内存管理，进程/线程
调度，虚拟文件系统，网络协议。。。从前开发过程中种种的疑惑都能够在这里找到最详实的答案。

当然Linux内核确实也非常艰深，费了很大功夫才摸到一些门道，现将最近阶段所学汇总，一来以备
复习只用，二来希望可以帮助其他学习者少走弯路。

![](/img/201903/linux_kernel_01.png)