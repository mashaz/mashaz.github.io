---
title: no internal routing support, rebuild with pcre support !!!解决方案
date: 2017-04-05 15:37:25
tags: centos
---

```bash
pip uninstall uwsgi
yum install -y pcre pcre-devel pcre-static
pip install uwsgi -I --no-cache-dir

```

* http://stackoverflow.com/questions/21669354/rebuild-uwsgi-with-pcre-support