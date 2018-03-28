---
title: 学习HTML
date: 2018-03-28 11:00:16
tags:
---

这篇文章是由以前学习HTML记录的小知识整理而来。<!-- more -->

## W3C诞生

W3C--万维网联盟，由www之父李爵士所创建的，该在组织通过制定标准来促进各个浏览器于html的兼容性以解决不同浏览器厂商不同的显示问题，此次html版本更新到第五代为html5。

## MDN组织
MDN--Mozilla开发文档，为Mozilla基金会产品和网络技术开发文档网站，它前身是网景公司，最后由一名mozilla员工创建成立的非营利性机构Mozilla基金会，提供各种网站开发技术及其技术文档，是前端开发工程师开发查询技术文档使用的网站。

## 文档声明
`<!DOCTYPE html>`

## 基本元素
html的三个基本元素: `html` `head` `body`，实际上在代码中是可以省略的。

由在W3C文档规范说明中找到，当省略以上三个元素时，浏览器在渲染时会默认补充。


## 语义化为主体
在HTML中是没有**块级**和**内联**元素这种说法的，因为在HTML中不可控制。这是CSS的表现形式决定的，所以并不建议了解HTML元素是不是块级和内联元素的区别。

在HTML中本身的意义，就是负责结构和语义，它并不管表现（这是CSS所做的）。要是HTML也有了表现的意义，那么它就不应该叫做或者不只是叫做超文本标记语言。有更加厉害的叫法叫什么超文本标记及表现语言等这类的，那么CSS的存在就是个累赘，也是不必要的存在。这也是为什么CSS会出现的原因。

## UA渲染
那么为什么只写了HTML，但是在浏览器中又会有块级、内联或者有字体大小、颜色的不同的区分呢？这就要回到之前说的，在浏览器中，它有着自己的一套CSS样式，当一个纯HTML文本在浏览器上打开时，检测到并无CSS，那么它就会强制将自己的CSS添加上当前的HTML并渲染。

## 浏览器纠正
在浏览器中的HTML会把你写错的元素或者格式进行纠正，而不进行报错

```html
在编辑器:
<head>
  <div>hello</div>
</head>

在浏览器变成:
<body>
 <div>
   hello
  </div> 
</body>
```
## 空标签
空标签，是html中的一个标签，指在标签中不存在内容或者元素，且空标签自身就是闭合的，不能再添加一个闭合标签。如`<br>`、`<img>`、`<input>`等。

## 可替换标签
可替换标签，为html中使用的对象资源决定，不能由css来决定使用的样式、资源等，如img、input、video标签等等。

## 本地测试HTML
在本地中打开的HTML文件，在浏览器的地址栏中可以看到使用的是一种**FTP**协议

![html-ftp](img/html-ftp.png)

使用这种协议有个缺点是，当默认使用这个协议时，若外部链接没有声明使用何种协议时，那么根据浏览器的渲染，也会默认将此协议当成FTP协议，如不加**HTTP**协议的链接`//qq.com`，没有表示当前链接是**HTTP**协议，那么此`href`的链接表示的是**FTP**协议，那么所带来的后果就是这个文件并不存在(FTP协议时文件路径协议)。

  ```html
  <a href="//qq.com">qq</a>

  因为是在本地电脑用浏览器打开的，此时的协议是ftp协议，所以href地址会被识别成在本地有一个名为'qq.com'的文件需要跳转(当然这个文件是不存在的)
  ```

所以是不建议使用ftp协议，用下面的方式就可以改变这种情况：

安装插件`npm i -g http-server`将当前的文件路径识别为在当前服务器浏览html

就是将所谓file协议的路径变成http协议的路径=>127.0.0.1:8080

运行: `http-server -c -1`(数字1)

接着打开上述的文件，点击链接会跳转到一个腾讯页面，因为此时的协议经过插件的运行改成了使用http协议，那么href的链接也是变成了作为http的qq链接

## a元素
`contenteditable`属性表示当前内容可编辑

`download`属性表示一个下载链接，通常网上的下载行为皆有这个属性

**href**属性:
- `href=""`表示当前页面刷新

- `href="#"`表示页面变成锚点

- `href="?name=xxx"`表示发出一个get请求

- `href="javascript: alert(1);"`--JavaScript伪协议
  - 通常是`href="javascript:;"`表示不做任何相应请求(`#`其实就是一个请求)

在地址输入`javascript: 语句;`回车也会执行一段javascript代码

`a`元素请求的是get请求


## form元素
`form`标签请求的是get、post两种请求方式(默认是get请求，但通常是post)

get获取内容，post上传内容


**提交方式**
如果`form`标签里面没有`submit`标签或者是`input type=submit`标签那么是无法提交请求的

```html
<form action="xxx.html" method="post">
  <input type="submit" value="提交" name="submit">
</form>
```

> 注意：每个input标签必须要有name属性，让数据清晰传递，或者说name的值相当于是传递数据的键key

get请求会把相应地数据添加在地址栏的后缀上作为查询参数，当然是相应的FTP协议是不支持post请求的(跳转404错误)，需使用HTTP协议

**type属性**
有`target`属性，跟`submit`标签对应使用

`button`若没有明确`type`属性，那么会自动升级为`submit`标签(具有提交功能)，但是下面两种情况只能是作为**按钮**使用:

- 在`button`标签下的`type`属性声明为`button`值:
  `<button type="button" username="">button</button>`

- 在`input`标签下的`type`属性为`button`值：
  `<input type="button" value="button" username="">`

由此得出:**只要使用button作为值的情况下，那么这个标签就只能为按钮使用**

`button`是允许有子标签的


## input元素
`label`标签是和`input`标签关联的，具体表现为在不想只点击输入框才能输入文字，而是想在点击文字的时候自动跳转到输入框中(直接跳转)

```html
<label for="xxx">用户名</label>
<input type="text" id="xxx" name="usernama">
# 必须要有for属性和id属性值为一致

当点击'用户名'时，自动跳转到输入框中
```
有时候，有些人为了更简便一些使用了一些技巧，那就是老司机进化版:

```html
<label>用户名<input type="text" name="username"></label>
```
作用是跟上面的一样，省去了`for`属性和`id`属性

使用`type="checkbox"`必须要有`value`属性值，作为对应`name`属性键的值

`input type="checkbox" name="" value=""`

使用多个`radio`时需指定相同的`name`属性值，表示为同一组

```html
<input type="radio" name="fult" value="oriage">橘子
<input type="radio" name="fult" value="banana">香蕉
```

## select元素

```html
<select name="group">
  <option value="">1</option>
  <option value="1">1</option>
  <option value="2">2</option>
  <option value="3" disabled>3</option> #不能选中
  <option value="4" selected>4</option> #默认选中
</select>

<select name="" multiple>表示可以多选,在选中一个的情况下按住Ctrl再选其他的即可
</select>
```

textarea标签默认是可以在浏览器上随意拉动宽高这个现象的，想固定只能使用css来设置不能拉动`style="resize:none"`，宽高建议也是用css的width和height定义

## table元素

```html
<table border=1>
  <colgroup> #<colgroup>必须和<col>一起使用才有效
  	<col width=100> -- 第1列的宽度
    <col width=200> -- 第2列的宽度
    <col width=100> -- 第3列的宽度
    <col width=70>  -- 第4列的宽度
  </colgroup>
  <thead>
  	<tr>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
  <tfoot></tfoot>
</table>
  
如果将thead、tbody、tfoot的顺序调换的话，在浏览器中会自动纠正过来为正确的顺序: 
code-- tfoot > thead > tbody  ==>  browser-- thead > tbody > tfoot

相应地，如果在代码中省略了table标签，在浏览器上也是会自动添加进去的
但是如果省略了thead、tbody、tfoot标签，那么会被认为全部单元格都在tbody中，而且是按照代码的顺序显示单元格，不会纠正
  
想去掉border中间的空隙，使用css的border-collapse: collaps;即可
```



感谢阅读