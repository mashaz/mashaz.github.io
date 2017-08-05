---
title: centOS开启apache让外网访问：开启80端口
date: 2017-04-05 10:41:51
tags: linux
---

### 开启apache后只需iptables开启80端口便可成功让外网访问到
```bash
iptables -I INPUT 1 -i eth0 -p tcp --dport 80 -m state --state NEW,ESTABLISHED
-j ACCEPT
service iptables save
service iptables restart
```
