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