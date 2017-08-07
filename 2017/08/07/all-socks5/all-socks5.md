---
title: macOS下各种各样走socks5的方法
date: 2017-08-07 20:16:16
tags: macOS
---

## Homebrew设置socks5

由于Homebrew下载用的是curl, 我这有两种方法让curl走socks5

1. 设置.curlrc

```shell
echo 'socks5 = "127.0.0.1:1080"' >> ~/.curlrc
```

2. ss

```shell
export ALL_PROXY=socks5://127.0.0.1:1080
```
我给这条命令设置了alias，用起来还是蛮方便的

你可以```curl ip.cn```查看当前ip

## python requests走socks5
```python
pip install -U requests[socks]

import requests
resp = requests.get('http://go.to', 
                    proxies=dict(http='socks5://user:pass@host:port',
                                 https='socks5://user:pass@host:port'))
```

## git走socks5
```shell
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## youtube-dl走socks5
```shell
youtube-dl -f bestvideo+bestaudio/best  --proxy 'socks5://127.0.0.1' 
```

---

to be continued...