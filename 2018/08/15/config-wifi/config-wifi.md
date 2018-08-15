---
title: Linux命令行下配置连接Wifi
date: 2018-08-15 22:35:02
tags: Linux
---



## 情景

树莓派(Kali Linux)只记住了手机热点的wifi，无其他外设

## 解决方案

* ssh
* edit '''/etc/network/interfaces''', append the follow config
'''shell
auto wlan0
iface wlan0 inet dhcp
	wpa-ssid "ssid is your wifi name"
	wpa-psk "password"
'''
* restart
* done


