---
title: 将2个Django网站同时部署在CentOS(Nginx)上
date: 2017-06-09 17:46:35
tags: linux
---

* 在/etc/nginx/conf.d下新建一个Nginx	配置文件new_website.conf
```bash
server {
      listen       80;
      server_name  yourdomain.com;
      location  / {
          proxy_pass            http://127.0.0.1:4444; # 另外一个端口
          proxy_redirect        off;
          proxy_set_header      Host             $host;
          proxy_set_header      X-Real-IP        $remote_addr;
          proxy_set_header      X-Forwarded-For  $proxy_add_x_forwarded_for;
          client_max_body_size  10m;
      }
}
```
* Nginx配置更新
```bash
nginx -s reload
```

* 然后做和部署第一个网站相同的步骤就OK了
