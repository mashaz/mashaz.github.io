---
title: Github新增用户公钥后, git push失败返回403
date: 2017-10-23 21:49:27
tags: git
---

### 错误信息

```bash
$ git push -u origin master
error: The requested URL returned error: 403 Forbidden while accessing https://github.com/mashaz/xxx.git

fatal: HTTP request failed
```

### 解决方案

修改 ```.git/config```
把 形如 ```url = https://MichaelDrogalis@github.com/mashaz/xxx.git``` 修改为```url = ssh://git@github.com/mashaz/xxx.git```的格式

### 相关资料

[Stack Overflow](https://stackoverflow.com/questions/7438313/pushing-to-git-returning-error-code-403-fatal-http-request-failed)


