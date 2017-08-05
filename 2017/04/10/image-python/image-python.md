---
title: python Image库的一些图片裁剪操作
date: 2017-04-10 20:26:58
tags: python
---

* selenium截的网页全屏图免不了批量裁剪,下面使用Image库进行一些裁剪操作

```python

from PIL import Image

FileNames=os.listdir('images') #image文件夹
i = 0
for imgfile in FileNames:
	if imgfile!='.DS_Store' and imgfile!='orgin_croped':
		img = Image.open("images/%s"%(imgfile))
		region = (344,344,750,830)  #数字请自行调整
		print("图片宽{0}px,高{1}px".format(img.size[0],img.size[1]))
		#裁切图片
		cropImg = img.crop(region)
		cropImg.save('imagesCroped/%s'%(imgfile))
```