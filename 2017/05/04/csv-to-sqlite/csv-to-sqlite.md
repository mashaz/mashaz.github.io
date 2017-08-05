---
title: csv转换到sqlite3
date: 2017-05-04 23:04:41
tags: sql
---
```bash
sqlite3 target.sqlite3
sqlite3>.separator ","
sqlite3>.import target.csv 表名
```

