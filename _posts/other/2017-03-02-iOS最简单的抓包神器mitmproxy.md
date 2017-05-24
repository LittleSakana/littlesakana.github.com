---
layout: article
title: "抓包神器mitmproxy"
categories: other
excerpt: "iOS最简单的抓包神器mitmproxy"
ads: true
share: false
image:
---

## 安装

前提：要安装brew

```
1.安装mitmproxy
brew install mitmproxy

2.手机网络设置代理为电脑ip

3.手机打开http://mitm.it，安装证书

4.打开监控
mitmproxy  -b 192.168.35.182  -p 2386
```

## 使用

