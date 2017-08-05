---
title: CentOS 6 + Gunicorn + Nginx + Django 部署
date: 2017-04-12 18:41:27
tags: django
---


* 试了很多Django部署到CentOS,这种方法是自己唯一实现的。
* 照了很多教程做，遇到很多坑，自己一个个google摸索出来的。
* 这里把一些坑和要点记录一下，做个参考。
---

* nginx配置文件，位于/etc/nginx/conf.d/yourconfig.conf

```shell
 server {
      listen       80;
      server_name  yourdomain.com;
      location  / {
          proxy_pass            http://127.0.0.1:8000;
          proxy_redirect        off;
          proxy_set_header      Host             $host;
          proxy_set_header      X-Real-IP        $remote_addr;
          proxy_set_header      X-Forwarded-For  $proxy_add_x_forwarded_for;
          client_max_body_size  10m;
      }
}
```
* cd 到你的Django根文件夹

* vim ***/setting.py 修改为 DEBUG = False
> nohup gunicorn yourproject.wsgi:application -b 127.0.0.1:8000 --reload &

* 后台开启gunicorn , “ nohup ... & ”为后台执行命令

* 关闭gunicorn
> ps -ef | grep gunicorn    --获取gunicorn进程号pid
> kill -9 pid

* Nginx更改配置后重加载
> nginx -s reload
