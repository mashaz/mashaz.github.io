---
title: 记录自己Python Spider一些常用的函数和脚本
date: 2017-03-23 22:49:27
tags: python
---

#### Terminal输出Style

```python
STYLE = {
        'fore':
        {   # 前景色
            'black'    : 30,   #  黑色
            'red'      : 31,   #  红色
            'green'    : 32,   #  绿色
            'yellow'   : 33,   #  黄色
            'blue'     : 34,   #  蓝色
            'purple'   : 35,   #  紫红色
            'cyan'     : 36,   #  青蓝色
            'white'    : 37,   #  白色
        },
        'back' :
        {   # 背景
            'black'     : 40,  #  黑色
            'red'       : 41,  #  红色
            'green'     : 42,  #  绿色
            'yellow'    : 43,  #  黄色
            'blue'      : 44,  #  蓝色
            'purple'    : 45,  #  紫红色
            'cyan'      : 46,  #  青蓝色
            'white'     : 47,  #  白色
        },
        'mode' :
        {   # 显示模式
            'mormal'    : 0,   #  终端默认设置
            'bold'      : 1,   #  高亮显示
            'underline' : 4,   #  使用下划线
            'blink'     : 5,   #  闪烁
            'invert'    : 7,   #  反白显示
            'hide'      : 8,   #  不可见
        },
        'default' :
        {
            'end' : 0,
        },
}
'''带Style输出'''
def UseStyle(string, mode = '', fore = '', back = ''):

    mode  = '%s' % STYLE['mode'][mode] if STYLE['mode'].has_key(mode) else ''
    fore  = '%s' % STYLE['fore'][fore] if STYLE['fore'].has_key(fore) else ''
    back  = '%s' % STYLE['back'][back] if STYLE['back'].has_key(back) else ''
    style = ';'.join([s for s in [mode, fore, back] if s])
    style = '\033[%sm' % style if style else ''
    end   = '\033[%sm' % STYLE['default']['end'] if style else ''
    return '%s%s%s' % (style, string, end)
```

#### 浏览器Cookies分割成标准格式

```python
def GetCookies():

	f = open('cookies.txt','r')
	cookies = {}
	for line in f.read().split(';'):
		name,value = line.strip().split('=',1)
		cookies[name] = value
	return cookies
```

#### CSV文件数据存入

```python
# -*- coding:utf-8 -*-
#!/usr/bin/env python
import sqlite3
import csv
import time
import sys
def main(pwd):
	conn = sqlite3.connect('douban_user.db')
	conn.text_factory = str
	cur = conn.cursor()
	cur.execute("CREATE TABLE if not exists users(username text, uid text , address text,addedTime text,follower integer)")
	with open( pwd, 'rb') as f:
	    reader = csv.reader(f)
	    for row in reader:
	    	row[3] = row[3].rstrip('加入').lstrip()
	    	if row[1]=='' :
	    		row[1]='unknown'
	    	cur.execute("INSERT INTO users VALUES (?,?,?,?,?)",(row[0],row[1],row[2],row[3],row[4]))
	    
	    conn.commit()
	    conn.close()    
	       
	f.close()

if __name__ == '__main__':
	pwd = sys.argv[1]
	main(pwd)
```

