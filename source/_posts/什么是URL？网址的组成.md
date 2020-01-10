---
title: 什么是URL？网址的组成
tags: http
categories: 前端知识
date: 2018-11-15 15:29:27
---
和 [Hypertext](https://developer.mozilla.org/en-US/docs/Glossary/Hypertext) 以及 [HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP) 一样，URL是Web中的一个核心概念。它是[浏览器](https://developer.mozilla.org/en-US/docs/Glossary/Browser)用来检索web上公布的任何资源的机制。

URL指的是统一资源定位符（Uniform Resource Locator）。URL无非就是一个给定的独特资源在Web上的地址。理论上说，每个有效的URL都指向一个独特的资源。这个资源可以是一个HTML页面，一个CSS文档，一幅图像，等等。而在实际中，有一些例外，最常见的情况就是URL指向了不存在的或是被移动过的资源。由于通过URL呈现的资源和URL本身由Web服务器处理，因此web服务器的拥有者需要认真地维护资源以及与它关联的URL。
 <!--more-->

 > 欢迎加入前端交流群来获取视频资料以及前端学习资料：[749539640](//shang.qq.com/wpa/qunwpa?idkey=f528775f242a7c39fe8512383febb8990e621bf97354c2fb82f6832097b7c501) 
一些URL的示例：

```
https://developer.mozilla.org
https://developer.mozilla.org/en-US/docs/Learn/
https://developer.mozilla.org/en-US/search?q=URL
```
一个URL由不同的部分组成，其中一些是必须的，而另一些是可选的。让我们以下面这个URL为例看看其中最重要的部分：

```
http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument

```
<img src="mdn-url-protocol@x2.png"  >


http:// 是协议。它表明了浏览器必须使用何种协议。它通常都是HTTP协议或是HTTP协议的安全版，即HTTPS。Web需要它们二者之一，但浏览器也知道如何处理其他协议，比如mailto:（打开邮件客户端）或者 ftp:（处理文件传输），所以当你看到这些协议时，不必惊讶。

<img src="mdn-url-domain@x2.png"  >

www.example.com 是域名。 它表明正在请求哪个Web服务器。或者，可以直接使用IP address, 但是因为它不太方便，所以它不经常在网络上使用。.

<img src="mdn-url-port@x2.png"  >


:80 是端口。 它表示用于访问Web服务器上的资源的技术“门”。如果Web服务器使用HTTP协议的标准端口（HTTP为80，HTTPS为443）来授予其资源的访问权限，则通常会被忽略。否则是强制性的。

<img src="mdn-url-path@x2.png"  >


/path/to/myfile.html 是网络服务器上资源的路径。在Web的早期阶段，像这样的路径表示Web服务器上的物理文件位置。如今，它主要是由没有任何物理现实的Web服务器处理的抽象。

 

<img src="mdn-url-parameters@x2.png"  >


?key1=value1&key2=value2 是提供给网络服务器的额外参数。 这些参数是用 & 符号分隔的键/值对列表。在返回资源之前，Web服务器可以使用这些参数来执行额外的操作。每个Web服务器都有自己关于参数的规则，唯一可靠的方式来知道特定Web服务器是否处理参数是通过询问Web服务器所有者。

<img src="mdn-url-anchor@x2.png"  >


#SomewhereInTheDocument 是资源本身的另一部分的锚点. 锚点表示资源中的一种“书签”，给浏览器显示位于该“加书签”位置的内容的方向。例如，在HTML文档上，浏览器将滚动到定义锚点的位置;在视频或音频文档上，浏览器将尝试转到锚代表的时间。值得注意的是，＃后面的部分（也称为片段标识符）从来没有发送到请求的服务器。

参考：[什么是url](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_URL)