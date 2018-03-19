---
title: CSS布局小结
date: 2018-03-19 16:20:47
tags:
---



​	在网页中，我们经常看到不同的网页多种展现页面的方式，这也是未来要去学习和构建的知识，所以现在在这里先整理一点布局的知识，以后会慢慢更新。<!--more-->

## 1.左右布局--两列布局

​	要构建两列布局还是比较容易的，其中比较常用的方法就是**浮动**，通过使用浮动将两个divs脱离文档流，自定义好width即可实现两列布局，需注意的是要在两者的父元素加上清除浮动的属性**clearfix**，使得这个结构不会影响到外部其余元素。

```html
<!-- 为省篇幅，只留下关键代码 -->

<section class="container">
  <div class="left-half">
    <h1>
      Left Half
    </h1>
  </div>
  <div class="right-half">
    <h1>
      Right Half
    </h1>
  </div>
</section>
```

```css
* {
  box-sizing: border-box;
}

html,
body,
section,
div {
  height: 100%;
}

body {
  text-align: center;
}

h1 {
  font-size: 1.75rem;
}

/* 以下是重点 */

.left-half {
  float: left;
  width: 50%;
  background: red;
}

.right-half {
  float: right;
  width: 50%;
  background: blue
}

```

效果图为这样:

![left-right-layat](CSS布局小结\left-right-layat.png)



**拓展--右列固定，左列自适应**

​	要实现这种布局，首先是要在code中，右列应在左列前面，然后右列使用浮动，左列使用overflow隐藏即可。

```html
<div class="container">
  <div class="right">
    Right
  </div>
  <div class="left">
    Left
  </div>
</div>
```

```css
.container {
   height: auto;
   overflow: hidden;
   color: white;
}

.right {
    width: 180px;
    float: right;
    background: red;
}

.left {
    float: none;
    background: blue;
    width: auto;
    overflow: hidden;
}
```

效果图如下:

![left-right-float-overflow-layat](CSS布局小结\left-right-float-overflow-layat.png)



## 2.左中右布局--三列或多列布局

​	在这个三列布局中，常见的布局是左右列固定，中间不定宽或自适应布局。所以我们可以使用浮动左右两列和加上宽度，中间列使用margin分隔左右两列固定的宽度，剩余的宽度则为当前body减去两边的宽度。需要注意的是在code中，中间列应在右列的下方。

```html
<div class="container">
  <div class="left">
    <h1>
      Left
    </h1>
  </div>
  <div class="right">
    <h1>
      Right
    </h1>
  </div>
  <div class="middle">
    <h1>
      Middle
    </h1>
  </div>
</div>
```

```css
* {
  margin: 0;
  padding: 0;
}

#content{
  height:300px;
}
.left{
  width: 200px;
  height:100%;
  float: left;
  background-color: #00a0dc;
}

.middle{
  height:100%;
  margin-left:200px;
  margin-right: 300px;
  background-color: red;
}

.right{
  height:100%;
  width: 300px;
  float: right;
  background-color: #00a0dc;
}
```

![left-right-middle-layat](CSS布局小结\left-right-middle-layat.png)

> 注意，在实际代码中,middle是在right后面的，否则会造成right一直在第二行而无法与left和middle平行



​	上述的方法其实存在一些小bug的，其中，若不小心忘记了middle和right的位置，后果是灾难性的。所以有一种算是比较改良的办法是使用浮动+绝对定位，让左右列浮动，中间列绝对定位于父元素中。

```html
<div class="container">
  <div class="left">
    <h1>Left</h1>
  </div>
  <div class="middle">
    <h1>Middle</h1>
  </div>
  <div class="right">
    <h1>Right</h1>
  </div>
</div>
```

```css
*{
  margin: 0;
  padding: 0;
}

.container{
  position: relative;
  width:100%;
  height:300px;
}

.left{
  float: left;
  width: 200px;
  height:100%;
  background-color: yellow;
}

.middle{
  position: absolute;
  top:0;
  bottom:0;
  left:200px;
  right: 300px;
  background-color: red;
}

.right{
  float: right;
  height:100%;
  width: 300px;
  background-color: blue;
}
```

效果图如下:

![left-right-middle-layat-absolute](CSS布局小结\left-right-middle-layat-absolute.png)



​	另外现在的趋势是使用一个`flex`布局，这个布局目前是比较流行的，是在2012年发布出来的，现在浏览器都支持这个属性，不用加后缀。

```html
<div id="content">
    <div id="left"> </div>
    <div id="middle"></div>
    <div id="right"></div>
</div>
```

```css
*{
  margin: 0;
  padding: 0;
}
#content {
  display: flex;
  width: 100%;
  height: 200px;
}
#left {
  flex:0 0 200px;
  height: 100%;
  background-color: #f04d0d;
}
#middle{
  flex: 1;
  background-color: blue;
}
#right {
  flex:0 0 200px;
  height: 100%;
  background-color: #f04d0d;
}
```

效果图如下:

![left-right-middle-layat-flex](CSS布局小结\left-right-middle-layat-flex.png)

如果非要搞事，想兼容IE特别低的版本，那么一般使用多种兼容方式:

```
display: -webkit-box;
display: -moz-box;
display: -ms-flexbox;
display: -webkit-flex;
display: flex;
```



## 3.水平居中

- 内联元素水平居中

若要实现水平居中的元素为inline元素，那么需要在父元素上声明`text-align: center`即可居中

```html
<div class="divBlock">
  <span>This is an inline element</span>
</div>
```

```css
.divBlock {
  text-align: center;
}
```

- 块级元素水平居中

使块级元素水平居中的方法是使左右外边距为自动，需要注意的是此时的块级元素是没有声明宽度的

```html
<div class="divCenter">
  <span>This is an block element</span>
</div>
```

```css
.divCenter {
  margin: 0 auto;
}
```

- 多个块级元素水平居中

将多个块级元素的`display`属性声明为`inline-block`，然后使用内联元素水平居中的方法，在父元素上使用文本居中`text-align: center`

```html
<div class="container">
  <div class="centerInline">
    From block-level elements to inline elements
  </div>
  <div class="centerInline">
    From block-level elements to inline elements
  </div>
  <div class="centerInline">
    From block-level elements to inline elements
  </div>
</div>
```

```css
.container {
  text-align: center;
}

.centerInline {
  display: inline-block;
  margin: 0 2px;
}
```



## 4.垂直居中

- 内联元素垂直居中

  对于单个内联元素，想实现居中可通过内边距`padding: 30px 0`相同来使内容垂直居中

- 块级元素垂直居中

  使用绝对定位和负外边距和边距

  ```html
  <main>
    <div>
      I'm a block-level element with a fixed height, centered vertically within my parent.
    </div>
  </main
  ```

  ```css
  * {
    margin: 0;
    padding: 0;
  }

  body {
    background: #f06d06;
    font-size: 80%;
  }

  main {
    background: white;
    height: 300px;
    width: 300px;
    margin: 20px;
    position: relative;
  }

  main div {
    position: absolute;
    top: 50%; /* 这里需注意的是从main的top-50%下流动的 */
    left: 20px;
    right: 20px;
    height: 100px;
    margin-top: -70px; /* 将div尽量向top-50%的位置上 */
    background: black;
    color: white;
    padding: 20px;
  }
  ```



使用Flex布局或者是Grid布局可轻松实现水平和垂直居中布局，以后更新



本文章待续