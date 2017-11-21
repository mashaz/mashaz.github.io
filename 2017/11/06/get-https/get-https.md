---
title: Let's Encrypt SSL证书部署小记(HTTPS)
date: 2017-11-06 17:04:24
tags: HTTPS
---
### 环境

* CentOS 6 on Vultr
* python2.7
* git

### 准备工作

最好提前``` yum update ```一下，我没开始升级有报错 

[相关链接](https://community.letsencrypt.org/t/certbot-doesnt-work-with-centos-6-could-not-install-os-dependencies-aborting-bootstrap/25171)

开启80和443端口[https://mashaz.github.io/2017/04/05/apache-config/](https://mashaz.github.io/2017/04/05/apache-config/)

---

```
git clone https://github.com/letsencrypt/letsencrypt
cd letsencrypt
./letsencrypt-auto certonly --standalone --email admin@***.com -d ***.com -d www.***.com
```

执行完毕出现成功的提示信息，证书有效期为3个月。
我们会在"/etc/letsencrypt/live/***.com/"域名目录下有4个文件就是生成的密钥证书文件。
我使用的Nginx环境，那就需要用到fullchain.pem和privkey.pem两个证书文件。

### 配置Nginx

主要设置对80到443的转发
```
ssh不上去了，先push了到时候再继续写吧
```

