---
title: 自己常用的ffmpeg命令
date: 2017-05-07 15:20:32
tags: ffmpeg
---

* youtube-dl下来的高清youtube视频和音频是分离的，这时候需要
> ffmpeg -i audio.m4a -i video.webm  -y output.mp4
---

* 两个或多个视频文件合并
> ffmpeg -f concat -i file.txt -c copy output.mp4
---
* file.txt位于执行目录
> file '1.mp4'
> file '2.mp4'
---

* avi转mp4
> ffmpeg -i input.avi -vcodec copy -acodec copy output.mp4

