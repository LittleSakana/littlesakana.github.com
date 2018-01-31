---
layout: article
title: "Instruments使用之简单使用(译)"
categories: iOS
excerpt: "Instruments程序内置在Xcode里，最直接的打开方式就是通过Xcode启动。你也可以通过Dock、Launchpad、命令行直接打开。"
ads: true
share: false
image:
---

## 启动Instruments

Instruments程序内置在Xcode里，最直接的打开方式就是通过Xcode启动。你也可以通过Dock、Launchpad、命令行直接打开。

### 从Xcode直接启动Instruments

#### 通过Xcode工具栏启动

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/xcode_instruments_menu_2x.png)

#### 直接对打开的Xcode工程profile

* 点击`Product`->`Profile`

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/xcode_product_profile_menu_2x.png)

* 点击并按住`Run`按钮,然后选择`Profile`

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/xcode_toolbar_profile_menuitem_2x.png)

* 直接`Command+I`

Xcode编译工程，然后Instruments运行起来，会提示你选一个profile模板。如果你经常用同一个模板profile你的应用程序，你可以设置你的工程当你初始化profile的时候自动使用它。

#### 设置Xcode功能使用一个特定的profile模板

* 点击`Product`->`Scheme`->`Edit Scheme`，或者`Command+<`

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/xcode_product_scheme_edit_scheme_menu_2x.png)

* scheme编辑器弹出来

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/xcode_scheme_editor_dialog_2x.png)

* 点击左边的`Profile`
* 在`Info`下，点击`Instrument`，从选择框中选择你想要的profile模板。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/xcode_scheme_editor_instrument_popup_2x.png)

> 如果你选择的是`Ask on Lanch`，Instruments将会在你开始profile的时候展示出所有的模板。

Xcode编译你的工程，Instruments启动，开始使用你配置的模板profile你的工程。

### 从Dock启动

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/dock_xcode_contextualmenu_instruments_2x.png)

你可以把Instruments快捷方式加到Dock中，这是最快的加载方式。Instruments启动后在Dock中右击Instruments图标，把它保留在Dock中。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_dock_contextual_menu_options_keepindock_2x.png)

### 从Lanchpad启动

Launchpad自动显示驻留在您的应用程序文件夹中的应用程序。因为Instruments不在应用程序文件夹，它不在Lanchpad显示。你可以给Instruments取一个别名，然后把它放到应用程序文件夹下。

#### 把Instruments加入Lanchpad

* 启动Instruments
* 在Dock中右击Instruments图标，选择`Show in Finder`

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_dock_contextual_menu_options_2x.png)

* 把Option+Command+拖拽Instruments图标到应用程序文件夹
* Instruments的图标就显示在Lanchpad中了

### 通过命令行启动

你可以通过`open`命令启动任何一个在OS X中的应用程序。在命令行输入`open /Applications/Xcode.app/Contents/Applications/Instruments.app`，可以启动Instruments。

## 初识Instruments

Instruments有几个主要的窗口和弹出框。

### profile模板选择对话框

当Instruments启动的时候，你会看到一个模板列表供你选择。这个列表包含一些标准的模板和一些你自己创建的自定义模板。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_profilingtemplate_dialog_2x.png)

这个profile模板选择对话框包含以下基本的部分：

* **Target device list**: 点击这里选择你要profile的设备。
* **Target process list**: 点击这里选择你要profile的一个或多个进程。
* **Filter buttons**: 点击这些按钮下面会对应低显示“标准模板”、“自定义模板”、“最近使用的模板”。
* **Search field**: 输入一些字符来快速找到你想要的模板，通过模板的名字和描述查询。
* **Template list**: 模板列表，会随着你点击`filter button`或者在`search field`输入字符而改变。
* **Template description**: 一个你选中的模板的简单描述，帮助你决定你选择的模板是否能满足你的需求。
* **Choose button**: 点击选择按钮以选择的模板为基础来创建一个新的`profile document`。当你按下`Option`键的时候这个按钮会变成“Profile”，点击这个“Profile”按钮会马上生成一个以选择的模板为基础的`profile document`并使用当前的进程开始profile。
* **Open button**: 点击这个按钮来选择一个已经存在的`profile document`，而不是使用一个新的模板。
* **Cancel button**: 点击这个按钮关闭模板选择对话框。

### Trace Document 跟踪文档

跟踪文档用来管理和配置profile的工具，初始化数据采集，查看分析结果。你可以通过初始化启动Instruments并选择一个profile模板或者从Xcode、Dock、命令行初始化profile来创建一个跟踪文档。你也可以保存、重新打开配置跟踪工具和收集数据的跟踪文档。一个跟踪文档可以包含很多极其细节的信息，这些信息通过很多面板和区域展示给你。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_trace_document_2x.png)

#### Toolbar

Toolbar让你可以开始、暂停、停止profile，增加instrument，显示或隐藏一些面板等等。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_trace_document_toolbar_2x.png)

包含以下这些元素：

* **Profiling controls**: 开始、暂停、停止数据收集。
* **Target device list**: 选择你要profile的设备。
* **Target process list**: 选择你要profile的进程。
* **Activity viewer**:  显示当前跟踪的运行时间或者在Timeline面板中的检查位置。如果你的跟踪文档有多个数据也会在这里展示。
* **Add Instrument button (+)**: 显示或者隐藏模板库，包含一个可用的模板列表。在这里你可以选择单独的instrument，把它加入到你的跟踪文档中。
* **Strategy button**s: 控制在timeline面板中显示的信息类型

	+ **CPU**: 在timeline面板中展示CPU核心的列表。只在跟踪文档包含记录CPU数据的instrument时可用。
	+ **Instruments**: 在timeline面板中展示instrument和它对应的数据。
	+ **Threads**: 在timeline面板中展示线程和对应数据的列表。只在跟踪文档包含记录线程数据的instrument时可用。

* **View buttons**: 显示或隐藏详细面板和inspector

#### Timeline面板

Timeline面板展示的是给定跟踪记录的数据的图形摘要。在这个面板中，每个instrument、CPU核心、线程，都有自己的跟踪显示收集的数据的图表。

尽管这个面板的信息是只读的，你可以通过滚动数据，选择特定的区域进行更仔细的检查，对你感兴趣的点插入标识。你可以通过调整缩放级别或者修改记录设置来调整图形信息的展示。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_trace_document_timeline_pane_instruments_2x.png)

##### Instruments strategy视图

这是一个包含在你的跟踪文档的所有单个的instrument和它们收集的数据的列表。你可以从模板库中拖拽一个新的instrument到这个列表。如果你选择了列表中的一个instrument，你可以删除或者在inspector面板配置它。instrument列表在你创建一个跟踪文档时可见。

##### CPU strategy 视图

如果你的跟踪文档里的instrument包含CPU相关的数据，一个CPU核心和随着时间使用情况的列表就展示在这里。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_trace_document_timeline_pane_cpu_2x.png)

##### 线程strategy视图

如果你的跟踪文档里的instrument包含线程相关的数据，线程和线程的使用情况的列表会在这里展示。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_trace_document_timeline_pane_threads_2x.png)

#### 详情面板

这个面板显示你的跟踪文档里的instrument收集到数据的详细信息。当正在profile的时候，在Timeline面板中选择一个单独的instrument来看它收集到数据的详细信息。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_detail_pane_2x.png)

#### 导航条

在详情面板的顶部的导航条帮助你浏览收集到的数据。你可以用它来在不同类型和层级的数据之间进行切换。

![](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Art/instruments_detail_pane_navigation_bar_2x.png)

* **Instrument**: 当前在Timeline面板中选中的instrument的图标，点击这里可以查看这个instrument的控制台和运行错误信息。
* **Detail type list**: 允许你在不同数据类型之间切换，这里显示的选项根据你选的instrument会有很大的不同。对于很多instrument来说，这个列表包含数据汇总，一个调用树，一个控制台。
* **Detail tree**: 当你在详细信息面板中浏览数据时，跟踪你在层次结构中的位置。单击树的一个分支，将层次结构返回到相应的数据。
* **Filter field**: 允许你对收集到的数据进行筛选。单击filter的按钮可以看到其他的过滤选项。你还可以通过调整inspetor面板的显示设置来更广泛地过滤收集到的数据。