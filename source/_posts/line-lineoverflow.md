---
title: html单行、多行文本溢出隐藏
tags: html
categories: 前端知识
keywords:
  - html 
  - 单行
  - 多行
  - 多行文本溢出隐藏
  - 单行文本溢出隐藏
date: 2020-01-10 14:58:35
---
html文本移除应该如何进行隐藏并显示省略号呢？
<!--more-->

{% note success no-icon %}
欢迎加入前端交流群：[749539640](//shang.qq.com/wpa/qunwpa?idkey=f528775f242a7c39fe8512383febb8990e621bf97354c2fb82f6832097b7c501) 
{% endnote %}
## 单行文本溢出隐藏
```js
1 div{/* 单行溢出隐藏 */
2             width: 150px;
3             white-space: nowrap;
4             overflow: hidden;
5             text-overflow: ellipsis;
6 }
```
## 多行文本溢出隐藏
```js
1 div{/* 多行溢出隐藏 */
2             width: 150px;
              display: -webkit-box;
5             -webkit-box-orient: vertical;
6             -webkit-line-clamp: 3;
7             overflow: hidden;
8 }
```
注：

-webkit-line-clamp用来限制在一个块元素显示的文本的行数。 
为了实现该效果，它需要组合其他的WebKit属性。常见结合属性：
display: -webkit-box; 必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。
-webkit-box-orient 必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。
