---
layout: article
title: "Instruments使用之简介(译)"
categories: iOS
excerpt: "Instruments是一个Xcode工具集的一个部分，它是一个强大的灵活的性能分析和测试工具。"
ads: true
share: false
image:
---

## 关于Instruments

Instruments是一个Xcode工具集的一个部分，它是一个强大的灵活的性能分析和测试工具。它帮助你profile你的OS X和iOS APP、进程和设备，让你更好的理解和优化他们的表现和性能。从APP开发流程一开始就把Instruments加入到你的开发周期的工作流中会节省你后期找问题的时间。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_app_icon_2x.png)

在Instruments中，你使用被称作*instuments*的专门的工具来随着时间推移跟踪你的APP、进程和设备的不同方面。Instruments随着profile的进行收集数据，然后把结果的详细信息展示给你供你分析。

不像其他的性能和调试工具，Instruments允许你收集各种不同类型的数据，并且并排查看它们。这使得识别可能被忽略的趋势变得更加容易。例如，你的APP或许会展示由于多个打开网络连接引起的大幅度的内存增长，通过使用Allocations 和 Connections工具，你能够定位到那些导致内存快速增长的没有关闭的网络连接。

通过高效的试用Instruments，你可以：

1. 检查一个或多个APP或者进程
2. 检查设备特定的特性，比如WiFi和蓝牙
3. 使用模拟器或者真机进行profile
4. 创建自定义的DTrace instruments来分析系统和APP行为
5. 跟踪你的源代码中的问题
6. 对你的应用进行性能分析
7. 找到你的应用中的内存问题，如泄漏、废弃的内存和僵尸对象
8. 确定优化你的应用程序以提高效率的方法
9. 执行系统级的故障诊断
10. 把instrument配置保存为模板来使用

尽管Instruments被内置在Xcode中，它却是一个独立的应用程序，能够被独立使用。

## Instruments工作流

Instruments看起来是一个复杂的应用程序。它可以被用来收集关于你的APP的所有有用的信息，帮助你分析解决问题。然而，整个instrument的工作流相对简单，如下图

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_workflow_diagram_2x.png)

概括地说，它包括以下几个主要阶段：

1. 配置一个包含想要的instrument和设置的跟踪文档
2. 设定一个要profile的设备和APP
3. profile这个APP
4. 分析在profile过程中抓取到的数据
5. 修复你的源代码中存在的问题

### 知道什么时候使用Instruments

当你用Xcode测试你的APP，在你使用Instruments之前，先参考下图的调试导航仪。这些仪表提供了你的APP的CPU、内存、电量使用、等等的概要信息。通常情况下，这些信息可以供你解决一些常见的问题。当你要更加详细的分析时就需要使用Instruments了。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/xcode_cpu_gauge_2x.png)

## 关于这个系列的文档

为了帮助你快速找到你需要的信息，这份文档被组织成侧重于Instruments具体方便的内容。

* 第一部分侧重于使用Instruments。包括创建一个document，找到一个你需要的instrument，profile一个APP，分析数据等。
* 中间部分包含更加专业的任务，例如提高性能，解决内存问题，提高电池的使用寿命。
* 最后的部分为个别的instrument和模板提供才考指引，还有一些资源文件和引导材料。

### 预备条件

在使用Instruments之前，你应该对Xcode如何工作的有比较深刻的理解，还有一些关键的APP开发概念，例如编译和运行一个APP，配置一个可供调试的真机设备。

你应该对你要profile的类型比较熟悉。例如你在查看你的APP的内存问题，你就应该知道一些关于内存管理和有可能的内存问题，例如泄漏和将是对象。如果你在查看你的APP的性能问题，你就需要知道一些关于CPU和线程使用的问题。如果你在尝试解决电池问题，你应该知道一些对电池造成一些负面影响的事情，里如果屏幕亮度、网络接口(GPS、蓝牙、WiFi)的使用，和计时器的使用。

本指南提供了关于这些主题和其他主题的一些背景信息。有关额外资源的连结可在以下网址找到:

[Related Documents](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/RelatedDocuments.html#//apple_ref/doc/uid/TP40004652-CH23-SW1)

[WWDC Videos](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/WWDCVideos.html#//apple_ref/doc/uid/TP40004652-CH24-SW1)

### 系统预备条件

Instruments是和Xcode一起安装的，如果你还没有安装Xcode，从Mac AppStore下载。

如果你打算在一个iOS设备上profile一个App，你需要配置你的设备。

> 注意：Instruments在Xcode3.0之后可用，需要OS X 10.5之后的操作系统。
> 
> Instruments能够profile iOS6之后的iOS设备。