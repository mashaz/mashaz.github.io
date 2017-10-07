---
title: Virtualenv修改目录后失效
date: 2017-10-08 06:02:33
tags: python
---

Virtualenv新建的时候脚本里环境变量就写死了，如果修改了与venv相关的父级目录名，```echo $PATH```一下就可以看得出环境变量出错了。
我试着把venv下所有旧目录名替换成新目录名，可以使用，暂时没有发生问题。