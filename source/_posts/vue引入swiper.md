---
title: vue引入swiper
tags: javascript
categories: 前端知识
date: 2017-04-09 22:57:16
---
{% asset_img logo.png This is an example image %}

### vue引入swiper  vue使用swiper  vue脚手架使用swiper /引入js文件/引入css文件

<!--more-->

> 欢迎加入前端交流群：[749539640](//shang.qq.com/wpa/qunwpa?idkey=f528775f242a7c39fe8512383febb8990e621bf97354c2fb82f6832097b7c501) 

----------------------------------------------------------

                  转载文章请注明出处！               

----------------------------------------------------------

 如果只是要使用轮播效果的话可以参考下一些vue组件；比如这篇文章

 

--------2019.7.9------------------

 

请参考swiper官方插件：[https://github.com/surmon-china/vue-awesome-swiper](https://github.com/surmon-china/vue-awesome-swiper)

 

--------2019.7.9------------------

 

 

#### 方法一：（ 请先使用这种方法；更新于2018-05-14）

下载swiper：
```javascript
npm install swiper --save-dev
```
swiper4.0使用入口：[http://www.swiper.com.cn/usage/index.html](http://www.swiper.com.cn/usage/index.html)；

### html：

 ```javascript
<div class="swiper-container">
    <div class="swiper-wrapper">
        <div class="swiper-slide">Slide 1</div>
        <div class="swiper-slide">Slide 2</div>
        <div class="swiper-slide">Slide 3</div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>
    
    <!-- 如果需要导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
    
    <!-- 如果需要滚动条 -->
    <div class="swiper-scrollbar"></div>
</div>
 ```

在需要使用swiper的组件里引入swiper，swiper的初始化放在mounted里（可以把官网例子的启动 var mySwiper =  删掉）；

### js：
 ```javascript
<script>
import Swiper from 'swiper';
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted(){
     new Swiper ('.swiper-container', {
    loop: true,
    // 如果需要分页器
    pagination: '.swiper-pagination',
    // 如果需要前进后退按钮
    nextButton: '.swiper-button-next',
    prevButton: '.swiper-button-prev',
    // 如果需要滚动条
    scrollbar: '.swiper-scrollbar',
  })        
  }
}
</script>
```
### css：

在main.js里引入css
```javascript
  import Vue from 'vue'
  import 'swiper/dist/css/swiper.css';
```
然后我们在用到swiper的组件里写点样式
```html
<style scoped>
 .swiper-container {
        width: 500px;
        height: 300px;
        margin: 20px auto;
    }
</style>
 ```

-----------------------------------我是分割线-----------------------------------------------------------

### 方法二：（以下是2017年4月写的,废弃）

1.安装vue-cli

参考地址：[https://github.com/vuejs/vue-cli](https://github.com/vuejs/vue-cli)

如果不使用严格语法需要在后三项打no；（加了挺头疼的，老是报错，但是对自己的代码规范性也是有很大的帮助的）

2.swiper下载示例代码

参考地址：[http://www.swiper.com.cn/usage/index.html](http://www.swiper.com.cn/usage/index.html)

一：单个组件使用：

3.在刚下载好的vue-cli里的helloworld.vue进行代码编写。

   ##### 3.1html部分：
```javascript
 1 <template>
 2   <div class="hello">
 3     <div class="swiper-container">
 4     <div class="swiper-wrapper">
 5         <div class="swiper-slide">Slide 1</div>
 6         <div class="swiper-slide">Slide 2</div>
 7         <div class="swiper-slide">Slide 3</div>
 8     </div>
 9     <!-- 如果需要分页器 -->
10     <div class="swiper-pagination"></div>
11     
12     <!-- 如果需要导航按钮 -->
13     <div class="swiper-button-prev"></div>
14     <div class="swiper-button-next"></div>
15     
16     <!-- 如果需要滚动条 -->
17     <div class="swiper-scrollbar"></div>
18 </div>
19   </div>
20 </template>
```
  #### 3.2 js部分：

这里使用import引入swiper.js文件；

swiper的启动放在mounted里执行；
```javascript
<script>
import'../assets/js/swiper.min.js'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted(){
     var mySwiper = new Swiper ('.swiper-container', {
    loop: true,
    // 如果需要分页器
    pagination: '.swiper-pagination',
    // 如果需要前进后退按钮
    nextButton: '.swiper-button-next',
    prevButton: '.swiper-button-prev',
    // 如果需要滚动条
    scrollbar: '.swiper-scrollbar',
  })        
  }
}
</script>
```
 ##### 3.3css部分：

 
```css
 1 <style scoped>
 2 @import'../assets/css/swiper.min.css';
 3     body {
 4         margin: 0;
 5         padding: 0;
 6     }
 7     .swiper-container {
 8         width: 500px;
 9         height: 300px;
10         margin: 20px auto;
11     }
12    
13 
14     </style>
 ```

4.看似大工告成，这时候会报错：
```
Uncaught TypeError: Cannot assign to read only property 'exports' of object '#<Object>'
```
这个错误查文档说是：

在webpack打包的时候，可以在js文件中混用require和export。但是不能混用import 以及module.exports。

因为webpack 2中不允许混用import和module.exports

我们只需要吧.babelrc文件里的第11行代码插件项"plugins": ["transform-runtime"],中的transform-runtime删掉即可；


```json
 1 {
 2   "presets": [
 3     ["env", {
 4       "modules": false,
 5       "targets": {
 6         "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
 7       }
 8     }],
 9     "stage-2"
10   ],
11   "plugins": [],
12   "env": {
13     "test": {
14       "presets": ["env", "stage-2"],
15       "plugins": ["istanbul"]
16     }
17   }
18 }
```
5.好了问题解决；

![](https://user-gold-cdn.xitu.io/2020/1/4/16f6c6310e966f77?w=670&h=584&f=bmp&s=1175076)

二：全局使用：

6.当然也可以全局使用swiper；代码如下；

还是在刚才的helloworld.vue进行代码编写；只是去掉js和css文件的引入！

helloworld.vue代码：
```javascript
 1 <template>
 2   <div class="hello">
 3     <div class="swiper-container">
 4     <div class="swiper-wrapper">
 5         <div class="swiper-slide">Slide 1</div>
 6         <div class="swiper-slide">Slide 2</div>
 7         <div class="swiper-slide">Slide 3</div>
 8     </div>
 9     <!-- 如果需要分页器 -->
10     <div class="swiper-pagination"></div>
11     
12     <!-- 如果需要导航按钮 -->
13     <div class="swiper-button-prev"></div>
14     <div class="swiper-button-next"></div>
15     
16     <!-- 如果需要滚动条 -->
17     <div class="swiper-scrollbar"></div>
18 </div>
19   </div>
20 </template>
21 
22 <script>
23 
24 export default {
25   name: 'HelloWorld',
26   data () {
27     return {
28       msg: 'Welcome to Your Vue.js App'
29     }
30   },
31   mounted(){
32      var mySwiper = new Swiper ('.swiper-container', {
33     loop: true,
34     // 如果需要分页器
35     pagination: '.swiper-pagination',
36     // 如果需要前进后退按钮
37     nextButton: '.swiper-button-next',
38     prevButton: '.swiper-button-prev',
39     // 如果需要滚动条
40     scrollbar: '.swiper-scrollbar',
41   })        
42   }
43 }
44 </script>
45 
46 <!-- Add "scoped" attribute to limit CSS to this component only -->
47 <style scoped>
48 
49     body {
50         margin: 0;
51         padding: 0;
52     }
53     .swiper-container {
54         width: 500px;
55         height: 300px;
56         margin: 20px auto;
57     }
58    
59 
60     </style>
```
main.js文件代码：
![](https://user-gold-cdn.xitu.io/2020/1/4/16f6c631106ff801?w=830&h=634&f=png&s=61090)


 常见报错解决：
```
Uncaught TypeError: Cannot assign to read only property 'exports' of object '#<Object>'
```
.babelrc文件里的插件项"plugins": ["transform-runtime"],中的transform-runtime删掉即可；

 

 

 

 



