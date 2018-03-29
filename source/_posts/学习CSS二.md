---
title: 学习CSS二
date: 2018-03-28 19:58:23
tags:
---

学习CSS永无止境<!-- more -->

## 导航下划线
使用`float: left`将每个`li`项浮动，设置`margin-left`和`margin-right`为不同项之间的间距，然后先设置`li`项的下划线`borger-bottom: 1px solid transparent`为透明色，就是表示先占一个位置，但是肉眼是看不出来的，然后在`a`项中使用伪类`:hover`再使用`borger-bottom: 1px solid red`将原先站位的透明色的下边框显示出来，这是一个鸡贼但是有效的方法。

在`li`中的`a`高度比`li`的要高，解决这个方法是设置`a`的css`display: block`即可。

在做导航条的时候，遇到使用`:hover`的情况，一般来说使用了`:hover`要在后面加一条下划线，这时不要用`text-decoration`这个属性，因为这个属性不能设置颜色和宽度，所以我们使用`border-bottom`这个属性，这是一个`a`标签，但是它是内联元素，就表示这个标签的范围不是扩充整个`li`标签的(`li`标签是块级元素)，所以要设置这个`a`的`display: block`。

但是这又引发了一个问题，就是前面在`a:hover`的时候会显示`border`，但是没有`hover`的时候，此时`a`的宽度是没有合算这个`border`的，所以当`:hover`的时候，宽度会加上`border-bottom`的宽度，从肉眼上看明显感到了当`:hover`的时候下面的内容也跟着向下移动了一般，那为了解决这个问题，我们是在`a`标签中也提前加上这个`border-bottom`，只不过是把颜色改为`transparent`，从肉眼上看这是没有`border`的，但是因为`a`本身已经添加了`border-bottom`，再`:hover`的时候只是将颜色显示出来，从而保证了没有`:hover`和`:hover`的元素宽度是一致的，不会感到内容向下移动的视觉出现。


## 脱离文档流
当一个`div`使用了`position：fixed`后，其子元素使用了`float:left`和`float：right`的会回缩在一起，解决这个问题的办法是使用`width:100%`就能解决到，但是又出现一个问题就是里面的子`div`感觉宽度正在变小一样，可以看出子`div`的宽度比以前要小，那么就要再父元素后面加一个`div`包裹这两个子`div`，再在这个`div`补上剩余的`padding`即可。

当下元素使用了`float`，父元素就要使用`clearfix`类，防止塌陷。

只有`display: block`的元素的`margin`上下会发生塌陷（只留下大的一方)其他情况(只要有一方是`inline-block`)上下的`margin`都会合计计算。


## 后代选择器和邻居选择器
请注意`footer.mdia` 和`footer  .media`的区别
`footer.mdia`是在一个标签上，而`footer .media`是一个父子标签

`footer.mdia`:
```html
<footer class="mdia"></footer>
```
`footer .mdia`:
```html
<footer>
	<div class="mdia"></div>
</footer>
```

## divs、spans宽度和高度

divs的高度取决于内容的实际高度，就是说包裹在其里面的元素，不过我现在有个spans声明了`margin`和`padding`的宽度，但是divs的高度还是内容的高度，是因为`margin`和`padding`是宽度的关系吗？如图所示:

![Snipaste_2018-03-14_14-52-47](\Snipaste_2018-03-14_14-52-47.png)

其中有红色边框的是divs，灰色边框的是spans，可以看到spans的`padding`延伸出来，但是divs的高度还是内容的高度。

为此，我在开发工具里面查看这个spans的高度发现是auto的:

![Snipaste_2018-03-14_15-03-35](\Snipaste_2018-03-14_15-03-35.png)

而且这个auto修改了其他值(比如50px)也不起任何作用，那么这就表明了inline元素是不具有宽度和高度的，之所以添加了边框感觉有其宽度和高度，但那是因为添加`padding`而已

但是如果将spans通过css转变为divs的话，divs的高度有占满了整个子元素的高度

![Snipaste_2018-03-14_15-01-17](\Snipaste_2018-03-14_15-01-17.png)

所以我们可以得知，divs下只有spans，且divs没有声明高度下，默认高度为spans的内容高度。那有什么取决于spans内容的高度呢？有两个: `font-size`和`line-height`。当`font-size`值越大时，内容的宽高自然在增大，此时的divs的高度也在增加；`line-height`可以粗暴的理解为spans的高度(但并不是，只是理解)，`ine-hieght`增大时，divs的高度也在增加。且当spans同时有这两个声明时，divs的高度取决于`line-height`的值。

总结:

- **inline元素不具有宽度和高度**

- **divs里面有spans元素，那么只计算这个元素的内容的高度**

- **inline元素有font-size和line-height属性会影响高度**

- **存在上述两个属性时，divs的高度优先取决于line-height**




## 边框盒子和内容盒子
`box-sizing: border-box`就是说指定了`width`后，总宽度就是`width`，包括在了`margin`和`paddin`g的宽度一起的，好处是不用计算宽度，就是`content-box`的宽度会变小

## 选择子标签
`:nth-child(odd/even)`

## 伪类和伪元素
`:xxx` 伪类

`::xxx`伪元素

`margin: 0 auto` 在没有宽度的情况下是没用的

## hack
使用了`display: inline-block`;会出bug，所以通常情况下下面应该接着使用`vertical-align:top`解决bug

错的事情多做几遍就知道为什么错了从而避免这个错

meta标签的charset=utf-8可不写，取决于后台能否自己指定这个charset

