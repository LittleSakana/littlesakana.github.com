---
layout: article
title: "cocoapods 初探"
categories: other
excerpt: "cocoapods 管理第三方开源库非常方便，使用过程中遇到一些坑，仅供参考"
ads: true
share: false
image:
---

## QA

#### pod search 获取不到最新版本，pod repo update 不管用

```
cd ~/.cocoapods/repos/master
git pull origin master
```