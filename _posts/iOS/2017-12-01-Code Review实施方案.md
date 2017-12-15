---
layout: article
title: "Code Review实施方案"
categories: iOS
excerpt: "代码review 如何实现? 如何贯穿在整个开发过程中? 如何保证上线代码都经过review? 看下具体实施方案吧"
ads: true
share: false
image:
---

## 一、总体方案

1. 收回代码权限由管理员统一管理。
2. 每次新版本开发申请一个分支，发布的时候使用，管理员将此分支设置为保护分支。
3. 每次合并到要发版本的分支，必须经过代码review，邮件到管理员及相关人员，发起merge request，才能被管理员同意合并，这样能保证每次合并的代码有人review过。

## 二、具体实施步骤

#### 1. 开辟新的发版分支

原则上在上次发版的master上拉取代码，不做任何修改创建一个新分支作为下次发版的新分支。

#### 2. 给管理员发邮件申请成为保护分支（如：feature1.2.0）

#### 3. 新建个人开发分支（如：zhangsan1.2.0）开发功能提交代码

#### 4. 切换到发版分支feature1.2.0，拉去最新代码

#### 5. 切换到自己的分支zhangsan1.2.0，合并发版分支的代码，push到远程

#### 6. 在gitlab网站发起merge request，从个人开发分支zhangsan1.2.0 合并到发版分支feature1.2.0

***注意：Assignee 选择要代码review的人员***

#### 7. (*建议*)reivew人员拉取开发人员代码分支，编译通过再进行review工作

#### 8. review结束，把Assignee设置为管理员

* 如果review没有问题，Assignee选择管理员，并在Comments里填写`review通过，可以合并`
* 如果review发现问题，则在Comments里写`review不通过，+ 具体原因`

#### 9. 管理员合并代码

如果合并发现有冲突等无法合并的情况，则驳回merge request，开发人员修改代码，重新发起merge request

#### 10. 流程图如下

![流程图](http://ono52urzb.bkt.clouddn.com/CodeReviewFlow.png)

## 三、注意问题

1. feature1.2.0上线结束，要打tag，代码要合并到master分支，然后再删除feature1.2.0
2. 如果线上出现问题，新建一个bugfix分支，分支名为bugfix+bug号
3. bugfix分支结束要合并到master分支，如果不是紧急bug不发版，也要合并到下个发版分支

## 四、常见问题汇总

1. 有部分代码和commit的描述无关
2. 一次commit包含太多内容，不太好review
3. 注释不规范或缺少注释
4. 单个方法代码超过150行
5. 使用了pod update 导致不相关类库更新到了新版，造成未知影响
6. 指定固定的第三方库版本，不允许使用波浪线等
7. pod库提交不完全，编译不通过