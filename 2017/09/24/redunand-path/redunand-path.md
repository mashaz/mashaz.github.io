---
title: macOS清理多余的环境变量
date: 2017-09-24 23:42:38
tags: macOS
---

以前安装过TeX，卸载了之后环境变量一直残留在$PATH。是不在.zshrc或者.bash_profile里的。进入``` /private/etc/paths.d```删除即可。