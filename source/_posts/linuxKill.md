---
title: LINUX查看端口占用并杀死(kill)的方式
cover_img: 'https://picsum.photos/300/201'
feature_img: 'https://picsum.photos/300/201'
index_img: 'https://picsum.photos/300/201'
top_img: 'https://picsum.photos/309/200'
cover: 'https://picsum.photos/309/200'
tags: javascript
categories: 前端知识
keywords:
  - 端口占用
  - linux
  - 杀死端口
date: 2020-06-05 14:11:16
---

### 查看端口占用

```vim
[root@VM_0_17_centos smartParsePro]#  netstat -tlnp|grep 1338
tcp6       0      0 :::1338                 :::*                    LISTEN      10447/node     
```

### 杀死端口

```vim
[root@VM_0_17_centos smartParsePro]# kill -9 10447
```
