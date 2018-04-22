---
title: scrapy设置http和socks5代理
date: 2018-04-22 21:18:04
tags: python
---


# scrapy设置http和socks5代理, 根据代理类型自动切换

scrapy的Request无法支持socks5代理，找了些资料写了个demo方便记录一下。
demo: https://github.com/mashaz/demos/tree/master/scrapy_proxy_demo

## 环境 

需要用到txsocksx这个module。
```shell
pip install txsockstx
```
> python2.7
> Scrapy (1.5.0)
> txsocksx (1.15.0.2)
> Twisted (17.9.0)

## 主要代码


* settings.py
```python
DOWNLOAD_HANDLERS = {
    "http": "scrapy_proxy_demo.proxy_switcher.Socks5DownloadHandler",
    "https": "scrapy_proxy_demo.proxy_switcher.Socks5DownloadHandler"
}
```


* new a file named proxy_switcher.py
```python
from txsocksx.http import SOCKS5Agent
from twisted.internet import reactor
#from scrapy.xlib.tx import TCP4ClientEndpoint # will be deprecated in future, import as the next line
from twisted.internet.endpoints import TCP4ClientEndpoint
from scrapy.core.downloader.webclient import _parse
from scrapy.core.downloader.handlers.http11 import HTTP11DownloadHandler, ScrapyAgent

class Socks5DownloadHandler(HTTP11DownloadHandler):
    def download_request(self, request, spider):
        """Return a deferred for the SOCKS5 or HTTP download"""
        if request.meta['proxy'].startswith('socks'):
            agent = ScrapySocks5Agent(contextFactory=self._contextFactory, pool=self._pool)
        else:
            agent = ScrapyAgent(contextFactory=self._contextFactory, pool=self._pool,
                maxsize=getattr(spider, 'download_maxsize', self._default_maxsize),
                warnsize=getattr(spider, 'download_warnsize', self._default_warnsize))

        return agent.download_request(request)

class ScrapySocks5Agent(ScrapyAgent):
    def _get_agent(self, request, timeout):
        bindAddress = request.meta.get('bindaddress') or self._bindAddress
        proxy = request.meta.get('proxy')
        if proxy:
            _, _, proxyHost, proxyPort, proxyParams = _parse(proxy)
            _, _, host, port, proxyParams = _parse(request.url)
            proxyEndpoint = TCP4ClientEndpoint(reactor, proxyHost, proxyPort,
                                timeout=timeout, bindAddress=bindAddress)
            agent = SOCKS5Agent(reactor, proxyEndpoint=proxyEndpoint)
            return agent
        return self._Agent(reactor, contextFactory=self._contextFactory,
            connectTimeout=timeout, bindAddress=bindAddress, pool=self._pool) 
```



#### 参考资料

https://gist.github.com/cydu/8a4b9855c5e21423c9c5
