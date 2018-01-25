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

### instrument

随着时间的推移，监视你的应用程序、过程或设备的不同方面。它收集数据把详细信息展示给你供你分析。一个跟踪文档`trace document`包含一个或多个instrument。

### library（instrument工具集）

一个展示可用instrument列表的窗口，可能会被植入到跟踪文档`trace document`。

### playhead

表示跟踪文档的时间轴窗格中的当前位置。拖动playhead可用及时地看到不同时间点记录的数据。

### profile

监视正在运行的app并抓取相关数据的动作。

### profiling template（profile模板）

包含一个包含一个或多个instrument的集合，通常被用来分析一个app，收集有用的信息，从而帮助定位问题或者让app更高效。

### run

一个app运行并被profile期间的会话。一个profile trace document能够抓取一系列的run，让你可以比较几次run的结果。

### strategy

能够在时间轴面板上看到的数据类型，包含CPU使用、instrument数据、和线程使用。

### target

一个你想用Instruments 来profile的设备和APP或者线程。

### timeline

一个随着时间推移图形化展示收集到的数据的面板。你可以移动在时间面板中的playhead来查看某个时间点收集到的数据。

### trace document

用来组织和配置profile的instruments，初始化数据收集，查看分析结果。



