---
title: scss常用整理
cover_img: 'https://picsum.photos/255/188'
feature_img: 'https://picsum.photos/255/188'
index_img: 'https://picsum.photos/255/188'
top_img: 'https://picsum.photos/255/188'
cover: 'https://picsum.photos/255/188'
tags: javascript
categories: 前端知识
keywords:
  - scss
date: 2020-04-23 11:39:43
---

本文整理了部分 scss 常用写作技巧

### 兼容各浏览器

```scss
@mixin prefix ($property, $value,
                 $moz:    true,
                 $webkit: true,
                 $o:      false,
                 $ms:     true,
                 $spec:   true) {
    @if $moz    {    -moz-#{$property}: $value; }
    @if $webkit { -webkit-#{$property}: $value; }
    @if $o      {      -o-#{$property}: $value; }
    @if $ms     {     -ms-#{$property}: $value; }
    @if $spec   {         #{$property}: $value; }
}

.bar-wrap {
  @include prefix(border-radius,10px 10px 10px 10px);
}
```

编译后

```css
.bar-wrap {
	-moz-border-radius:10px 10px 10px 10px;
	-webkit-border-radius:10px 10px 10px 10px;
	-ms-border-radius:10px 10px 10px 10px;
	border-radius:10px 10px 10px 10px;
}
```
