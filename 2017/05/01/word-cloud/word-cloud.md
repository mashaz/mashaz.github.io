---
title: 分词结果生成词云wordcloud
date: 2017-05-01 01:50:49
tags: python
---


### 最近和同学参加了个外包竞赛，涉及到评论的分析，词云是个不错的展示。


```python
from wordcloud import WordCloud,STOPWORDS,ImageColorGenerator
from scipy.misc import imread

sfile = open('jieba.txt','r')
text = sfile.read().decode('utf-8')
bg_img = imread('bg.png') #词云背景图,可无

wc_with_bg = WordCloud(
	background_color = 'white',    # 设置背景颜色
   	mask = bg_img,        # 设置背景图片
   	max_words = 2000,            # 设置最大现实的字数
   	stopwords = STOPWORDS,        # 设置停用词
   	font_path = '/Library/Fonts/Arial Unicode.ttf', # 设置字体格式，如不设置显示不了中文，我这里为Mac下的字体
   	max_font_size = 50,            # 设置字体最大值
   	random_state = 30,            # 设置有多少种随机生成状态，即有多少种配色方案

wc_with_bg.generate(text)

# plt.imshow(wc)
# plt.axis('off')
# plt.show()
# 显示

wc_with_bg.to_file('%s.jpg'%(name)) # 保存到当前路径
```
<img src="http://i.imgur.com/Ez2SNuT.jpg" title="img" />
