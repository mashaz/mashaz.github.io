---
title: SSH免密码登录
date: 2017-05-15 17:56:26
tags: ssh
---
* 本地环境 macOS
* 服务器 CentOS 6

1. 在Mac中打开终端，切换到当前目录的~/.ssh目录下，查看是否已经存在key，如下图，如果存在id_rsa.pub文件，则可以跳过第2步直接看第3步，如果不存在请看第2步。
```bash
cd ~/.ssh
ls
```

2. 生成RSA密钥，输入以下命令，其中邮箱地址选填写，然后连按3次回车，表示在默认路径生成，空密码。
```bash
ssh-keygen -t rsa -C "yourname@domain.com"
```

3. 复制密钥。切换到~/.ssh目录，打开id_rsa.pub文件，拷贝里面的一串内容。
```bash
vi ~/.ssh/id_rsa.pub
```
    其中，拷贝的那串内容长这样“ssh-rsa AAAAB3NzaC1yc2….”

4. ssh连接到你的服务器，然后同样切换到~/.ssh目录，如果没有这个目录，就使用mkdir .ssh命令创建一个，然后在authorized_keys文件里追加刚才拷贝的内容，保存然后退出ssh连接。
```bash
vi ~/.ssh/authorized_keys
```
    至此，免密码登陆已经实现