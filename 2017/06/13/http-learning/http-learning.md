---
title: HTTP协议随手记
date: 2017-06-13 17:16:30
tags: HTTP
---
* HTTP主要特点
1. 支持客户／服务器模式
2. 无连接
3. 无状态
### HTTP请求
* HTTP请求由三部分组成
1. 请求行
2. 消息报头
3. 请求正文

* 请求报头 eg
```bash
GET /form.html HTTP/1.1 (CRLF)
Accept:image/gif,image/x-xbitmap,image/jpeg,application/x-shockwave-flash,application/vnd.ms-excel,application/vnd.ms-powerpoint,application/msword,*/* (CRLF)
Accept-Language:zh-cn (CRLF)
Accept-Encoding:gzip,deflate (CRLF)
If-Modified-Since:Wed,05 Jan 2007 11:21:25 GMT (CRLF)
If-None-Match:W/"80b1a4c018f3c41:8317" (CRLF)
User-Agent:Mozilla/4.0(compatible;MSIE6.0;Windows NT 5.0) (CRLF)
Host:www.guet.edu.cn (CRLF)
Connection:Keep-Alive (CRLF)
(CRLF)
```
### HTTP响应
* HTTP响应由三部分组成
1. 状态行
2. 消息报头
3. 响应正文

* 状态码
> 1xx：指示信息--表示请求已接收，继续处理

> 2xx：成功--表示请求已被成功接收、理解、接受

> 3xx：重定向--要完成请求必须进行更进一步的操作

> 4xx：客户端错误--请求有语法错误或请求无法实现

> 5xx：服务器端错误--服务器未能实现合法的请求

