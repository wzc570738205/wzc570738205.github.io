---
title: 前端异步加载js
cover_img: 'https://picsum.photos/333/195'
feature_img: 'https://picsum.photos/333/195'
index_img: 'https://picsum.photos/333/195'
top_img: 'https://picsum.photos/333/195'
cover: 'https://picsum.photos/333/195'
tags: javascript
categories: 前端知识
keywords:
  - js
  - 前端
  - 异步加载js
date: 2020-05-06 13:15:15
---

欢迎加入前端交流群：[749539640](//shang.qq.com/wpa/qunwpa?idkey=f528775f242a7c39fe8512383febb8990e621bf97354c2fb82f6832097b7c501) 
## JavaScript阻塞
JavaScript在浏览器中的性能，可以认为是所有开发者所要面的的最重要的可用性问题。此问题因JavaScript的阻塞特性而复杂，也就是说，当JavaScript运行时其他的事情不能被浏览器处理。事实上，大多数浏览器使用单进程处理UI和更新JavaScript运行等多个任务，而同一时间只能有一个任务被执行。JavaScript运行了多长时间，那么在浏览器空闲下来相应用户输入之前的等待的时间就有多长

从基本层面说，这意味着```<script>```标签的出现使整个页面因脚本解析、运行而出现等待。不论实际的JavaScript代码是内联还是包含在一个不相干的外部文件中，页面下载和解析过程必须停下，等待脚本完成这些处理，然后才能继续。比如下面这段代码

```html
<html>
      <head>
        <title>Script Example</title>
      </head>
      
      <body>
        <p>
          <script type="text/javascript">
              document.write("The date is " + (new Date()).toDateString());
          </script>
        </p>
      </body>
</html>

```
 当浏览器遇到```<script>```标签时，无法预知JavaScript是否在```<p>```标签中添加内容。因此，浏览器停下来，运行此JavaScript代码，然后再继续解析、渲染页面。同样的事情发生在使用```src```属性加载JavaScript的过程中。浏览器必须先下载外部文件的代码，这要占用一些时间，然后解析并运行此代码。这个过程，页面解析和用户交互式完全被阻塞的。

 ## 更改脚本位置
 HTML.4文档指出，一个```<script>```标签可以放在```<HTML>```或```<body>```标签中，可以在其中多次出现。传统上，```<script>```标签用于加载外部JavaScript文件。```<head>```部分除此类代码外，还包含```<link>```标签用于加载外部```CSS```文件和其他页面中间件。也就是说，最好把风格和行为所依赖的部分放在一起，首先加载她们，使得页面可以得到正确的外观和行为，比如：
```html
<html>
  <head>
    <title>Script Example</title>
    <script type="text/javascript" src="file1.js"></script>
    <script type="text/javascript" src="file2.js"></script>
    <script type="text/javascript" src="file3.js"></script>
    <link rel="stylesheet" type="text/css" href="styles.css" />
  </head>
  <body>
    <p>Hello world!</p>
  </body>
</html>

```
虽然这些代码看起来没什么问题，但他确实存在性能问题；在```<head>```部分加载了多个JavaScript文件。因为每个```<JavaScript>```文件标签阻塞了页面的解析过程，知道它完整的下载并运行了外部JavaScript代码之后，页面处理才能行继续进行。用户比必须忍受这种可以察觉的延迟。强调一点，浏览器遇到```<body>```标签之前不会渲染页面的任何部分。用这种方法把脚本放在页面的顶端，将导致一个可以察觉的延迟，通常表现为：页面打开时，首先显示为一副空白的页面，而此时用户既不能阅读，也不能与页面进行交互操作。

因为脚本阻塞其他页面资源的下载过程，所以推荐的办法是：将所有的```<script>```标签放在尽可能接近```<body>```标签底部的位置，尽量减少对整个页面下载的影响。如：

```html
<html>
  <head>
    <title>Script Example</title>
    <link rel="stylesheet" type="text/css" href="styles.css" />
  </head>
  <body>
    <p>Hello world!</p>
    <script type="text/javascript" src="file1.js"></script>
    <script type="text/javascript" src="file2.js"></script>
    <script type="text/javascript" src="file3.js"></script>
  </body>
</html>

```
## 成组脚本
由于每个```<script>```加载都会阻塞页面解析过程，所以限制页面的```<script>```总数也可以改善性能。这个规则对内联脚本和外部脚本同样适用。每当页面接续碰到一个```<script>```标签时，紧接着有一段时间用于代码执行。最小化这些延迟时间将可以改善页面的整体性能。

## 非阻塞脚本


 ### 延时脚本