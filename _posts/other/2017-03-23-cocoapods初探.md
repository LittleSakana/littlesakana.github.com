---
layout: article
title: "cocoapods 初探"
categories: other
excerpt: "cocoapods 管理第三方开源库非常方便，使用过程中遇到一些坑，仅供参考"
ads: true
share: false
image:
---

## Podfile详解

Podfile是一个或多个工程项目的target依赖的说明文件。这个文件应该被命名为Podfile，我们以cocoapods1.0 举例。CocoaPods是用ruby实现的，因此Podfile文件的语法就是ruby的语法。

### 一个非常简单的Podfile文件

```
target 'MyApp' do
  use_frameworks!
  pod 'Alamofire', '~> 3.0'
end
```

### 一个复杂的Podfile文件

```
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/Artsy/Specs.git'

platform :ios, '9.0'
inhibit_all_warnings!

target 'MyApp' do
  pod 'GoogleAnalytics', '~> 3.1'

  # Has its own copy of OCMock
  # and has access to GoogleAnalytics via the app
  # that hosts the test target

  target 'MyAppTests' do
    inherit! :search_paths
    pod 'OCMock', '~> 2.0.1'
  end
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    puts target.name
  end
end
```

### 如果多个target想公用相同的pods，请使用abstract_target

```
# There are no targets called "Shows" in any Xcode projects
abstract_target 'Shows' do
  pod 'ShowsKit'
  pod 'Fabric'

  # Has its own copy of ShowsKit + ShowWebAuth
  target 'ShowsiOS' do
    pod 'ShowWebAuth'
  end

  # Has its own copy of ShowsKit + ShowTVAuth
  target 'ShowsTV' do
    pod 'ShowTVAuth'
  end
end
There is implicit abstract target at the root of the Podfile, so you could write the above example as:

pod 'ShowsKit'
pod 'Fabric'

# Has its own copy of ShowsKit + ShowWebAuth
target 'ShowsiOS' do
  pod 'ShowWebAuth'
end

# Has its own copy of ShowsKit + ShowTVAuth
target 'ShowsTV' do
  pod 'ShowTVAuth'
end
```

### 指定第三方库的版本号

#### 初始时获取最新版本，不指定版本号

```
pod 'AFNetworking'
```

#### 指定特定版本，以免误更新导致第三方库冲突

```
pod 'AFNetworking','3.1.0'
```

#### 除了不指定和指定一个特定的版本号，还可以使用逻辑运算符

* `> 0.1` 大于0.1的任何版本
* `>= 0.1` 大于等于0.1的任何版本
* `< 0.1` 小于0.1的任何版本
* `<= 0.1` 小于等于0.1的任何版本

#### 还有改进的逻辑运算符`~>`

* `~> 0.1.2` 大于等于0.1.2，小于2.0的版本
* `~> 0.1` 大于等于0.1，小于1.0的版本
* `~> 0` 版本号大于0，和不写是一样的

#### 指定到源码库的master分支

```
pod 'Alamofire', :git => 'https://github.com/Alamofire/Alamofire.git'
```

#### 指定到源码库的其他分支

```
pod 'Alamofire', :git => 'https://github.com/Alamofire/Alamofire.git', :branch => 'dev'
```

#### 指定到源码库的某个tag

```
pod 'Alamofire', :git => 'https://github.com/Alamofire/Alamofire.git', :tag => '3.1.1'
```

#### 指定到源码库的某次提交

```
pod 'Alamofire', :git => 'https://github.com/Alamofire/Alamofire.git', :commit => '0f506b1c45'
```

## Podfile.lock文件

* 当团队中的某个人执行完pod install命令后，生成的Podfile.lock文件就记录下了当时最新Pods依赖库的版本。
* 这时团队中的其它人check下来这份包含Podfile.lock文件的工程以后，再去执行pod install命令时，获取下来的Pods依赖库的版本就和最开始用户获取到的版本一致。
* 如果没有Podfile.lock文件，后续所有用户执行pod install命令都会获取最新版本的SBJson，这就有可能造成同一个团队使用的依赖库版本不一致。
* Podfile.lock文件对团队协作如此重要，我们需要将它添加到版本管理中。

## Cocoapods常用命令

### pod install

根据Podfile文件指定的内容，安装依赖库，如果有Podfile.lock文件而且对应的Podfile文件未被修改，则会根据Podfile.lock文件指定的版本安装。每次更新了Podfile文件时，都需要重新执行该命令，以便重新安装Pods依赖库。

### pod update

如果Podfile中指定的依赖库版本不是写死的，当对应的依赖库有了更新，无论有没有Podfile.lock文件都会去获取Podfile文件描述的允许获取到的最新依赖库版本。

### pod search

搜索第三方库在本地依赖库的版本，格式为 `pod search xxx`

### pod setup

这条命令用于跟新本地电脑上的保存的Pods依赖库。由于每天有很多人会创建或者更新Pods依赖库，这条命令执行的时候会相当慢，还请耐心等待。我们需要经常执行这条命令，否则有新的Pods依赖库的时候执行pod search命令是搜不出来的。
 
## QA

#### pod search 获取不到最新版本，pod repo update 不管用,怎么办？

```
cd ~/.cocoapods/repos/master
git pull origin master
```