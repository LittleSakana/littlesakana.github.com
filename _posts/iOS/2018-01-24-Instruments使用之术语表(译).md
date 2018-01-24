---
layout: article
title: "Instruments使用之术语表"
categories: iOS
excerpt: "想要使用好Instruments，先了解一下术语，要不然看不懂。"
ads: true
share: false
image:
---

### deferred mode(延迟模式)

以`deferred mode`(延迟模式)运行Instruments会延迟分析数据知道数据收集完成，无论是你已经完成运行还是你点了Stop按钮。当你在`deferred mode`(延迟模式)的并且它在手机数据的时候，你和Instruments的交互行为会被阻塞。

### DTrace

一个有Sun公司最初创建并一直到OS X上的动态跟踪工具。DTrace进入操作系统内核，提供对在你的计算机上运行的用户进程和内核的底层信息的访问。很多内置在Instruments中的工具都基于DTrace。DTrace本身是一个复杂的工具，但是Instruments提供了一个简单的接口让你访问DTrace的强大功能而不去管它的复杂性。想要了解更多DTrace和D脚本语言，请移步[Solaris Dynamic Tracing Guide](http://docs.oracle.com/cd/E19253-01/817-6223/)。
