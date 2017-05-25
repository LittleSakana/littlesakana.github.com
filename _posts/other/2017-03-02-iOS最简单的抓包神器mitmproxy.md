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

1. 在vps上启动mitmproxy `mitmproxy -b xxx.xxx.xxx（指定监听的接口） -p xxx（指定端口）`
2. 上下键定位请求
3. 回车键进入请求
4. `h` 向前， `l` 向后， `h` 向下， `k` 向上,选中request、response、detail
5. 按`e`进入编辑状态，然后按对应的蓝色字体来选择修改的部分
6. `esc`保存，`q`返回上一级
7. 修改完后，按`r`重新发起请求


