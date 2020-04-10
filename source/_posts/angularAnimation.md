---
title: Angular动画
tags: javascript
categories: 前端知识
cover_img: 'https://picsum.photos/302/202'
feature_img: 'https://picsum.photos/302/202'
index_img: 'https://picsum.photos/302/202'
keywords:
  - angular
  - animation
  - animations
  - Angular动画
  - angular animation
  - angular animations
date: 2020-01-16 11:01:54
---
<p class="note note-primary">原生实现</p>

如果不使用框架的话我们在浏览器中使用动画无非2种
- css实现
- js实现

#### css实现
我们可以使用基于css3的一个动画库，[Animate.css](https://daneden.github.io/animate.css/)
这样可以实现动画，但是不太好控制它的行为
<!-- more -->
#### javascript实现
如果为了实现更复杂的动画，更好的控制，我们可以使用js来实现动画
比如使用
- [jquery](http://jquery.cuishifeng.cn/show.html)
- [GSAP](https://www.npmjs.com/package/gsap)
- [Zepto](https://zeptojs.com/)
- [Web Animations Api](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Animations_API)


<p class="note note-primary">Angular中使用</p>

[官方文档](https://angular.io/guide/animations)

典型的动画会涉及多种随时间变化的转换。HTML 元素可以移动、变换颜色、增加或缩小、隐藏或从页面中滑出。 这些变化可以同时发生或顺序发生。你可以控制每次转换的持续时间。

Angular 的动画系统是基于 CSS 功能构建的，这意味着你可以 "动" 浏览器认为可动的任何属性。包括位置、大小、变形、颜色、边框等。W3C 在它的 [CSS Transitions](https://www.w3.org/TR/css-transitions-1/) 页中维护了一个可动属性的列表。

angular动画大体分为四部分
- trigger()
- transition()
- state()
- animate()

#### trigger
创建一个有名字的动画触发器，包含一个 state() 和 transition() 的列表，当此触发器的绑定表达式发生变化时，它们就会重新求值。

#### state
在附加到元素的触发器上，声明一个动画状态。
默认状态为```void```,简称无状态
#### transition
声明一个转场动画，以便在满足给定条件时运行一系列动画步骤。该条件是一个逻辑型表达式或一个函数， 该函数比较以前和现在的动画状态，如果应该开始转场则返回 true。 当满足所定义的转场动画的状态标准时，就会开始执行相关的动画。
#### animate
定义一个动画步骤，它把一些样式信息和时序信息组合在一起。

[示例demo](https://stackblitz.com/edit/angulartransition)
app.component.ts
<!-- tab app.component.ts -->
```js
@Component({
  selector: 'app-app',
  animations: [
    trigger('openClose', [
      // ...
      state('open', style({
        height: '200px',
        opacity: 1,
        backgroundColor: 'yellow'
      })),
      state('closed', style({
        height: '100px',
        opacity: 0.5,
        backgroundColor: 'green'
      })),
      transition('open => closed', [
        animate('1s')
      ]),
      transition('closed => open', [
        animate('0.5s')
      ]),
    ]),
  ],
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.css']
})
export class OpenCloseComponent {
  isOpen = true;
 
  toggle() {
    this.isOpen = !this.isOpen;
  }
 
}
```
<!-- endtab -->
<!-- tab app.component.html -->
app.component.html
```html
<div [@openClose]="isOpen ? 'open' : 'closed'" class="open-close-container">
  <p>The box is now {{ isOpen ? 'Open' : 'Closed' }}!</p>
</div>
```
<!-- endtab -->
<!-- tab app.component.css -->
app.component.css
```css
:host {
  display: block;
}

.open-close-container {
  border: 1px solid #dddddd;
  margin-top: 1em;
  padding: 20px 20px 0px 20px;
  color: #000000;
  font-weight: bold;
  font-size: 20px;
}
```
<!-- endtab -->