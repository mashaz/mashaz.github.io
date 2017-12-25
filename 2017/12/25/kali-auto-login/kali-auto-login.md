---
title: 树莓派Kali Linux自动登录
date: 2017-12-25 19:03:08
tags: raspberry
---

网上一大堆Kali Linux for raspberry修改自动登录的中文教程实测又没效果，最新版kali好像修改了方式，终于找到了一个有用的

* Linux kali 4.4.50-v7+ #1 SMP Wed Aug 30 11:08:41 CDT 2017 armv7l GNU/Linux
* Raspberry 3 model b

```bash
## Kali light xfce4 root autologin (works after lightdm update)
# @author intrd - http://dann.com.br/ 
# @license Creative Commons Attribution-ShareAlike 4.0 International License - http://creativecommons.org/licenses/by-sa/4.0/

After lighdtdm update root autologin is broken fix doing this:
nano /etc/lightdm/lightdm.conf
  at [Seat:*] group uncomment/edit:
  autologin-user=root
  autologin-user-timeout=0

now..
nano /etc/pam.d/lightdm-autologin 
  change:
    auth      required pam_succeed_if.so user != root quiet_success
  to:
    auth      required pam_succeed_if.so user != anything quiet_success

all done! :)
```
