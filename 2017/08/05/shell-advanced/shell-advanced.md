---
title: shell-advanced
date: 2017-08-05 17:01:09
tags: shell
---

# Shell进阶

一直在用Python处理简单的文件任务，但比起Shell来，还是很繁琐。加上一直以来就想稍微加深一下Shell的理解运用，不如抽一个周六的午后，写一篇博文来记录一下。

ps.这里写一些自己常用的例子，具体每个命令很多参数还是要man一下。

pps.本文用的是shell是zsh。


### 统计文件名含有某关键词的文件数:
```
ls -LR | grep -i keyword | wc -l
# ls:
# -L 如是链接文件，显示指向的文件信息
# -R 递归子目录
# grep:
# -i 忽略大小写
# -e 使用正则表达式
# wc:
# -l 统计长度
```


### 删除某文件名的文件
```shell
find . -name '[a-z].txt' -maxdepth 1 -exec rm {} \;
# find:
# -name 文件名支持正则 
# -maxdepth 递归层数
```

```shell
touch {a..z}.txt
```