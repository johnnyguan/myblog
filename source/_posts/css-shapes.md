---
title: css shapes（译）
date: 2018-01-24 11:14:53
tags:
---
由 http://alistapart.com/article/css-shapes-101 翻译

矩形中套矩形：网页通常都是这个构成的。我们通过CSS创造[几何形状](https://css-tricks.com/examples/ShapesOfCSS/)来打破限制，但那些形状从未影响到被改变形状元素的内部。

````
新的CSS Shapes规范改变了这个。在2012年年中由Adobe引入，它的目的是为设计者提供一种新方式来改变在任意复杂形状内部及周围的内容流动。之前不能做到。
````
![Notice how the text wraps around the circular shape of a bowl in this example. Using CSS Shapes, we can create similar designs for the web.](shape-outside-example.jpg)
## Creating a CSS Shape
你可以使用Shapes的一个属性将shape应用到元素上。你将shape function作为值传给shape 属性。
![](shape-rule.png)
形状可以用以下函数中的一个来创建：
- circle()
- ellipse()
- inset()
- polygon()

接受以上值的形状属性有：
- shape-outside:在形状外包裹内容
- shape-inside:在形状内包裹内容**规范暂时不可使用**

你可以结合*shape-margin*使用*shape-outside*，从而在shape外面增加外边距。对一个元素声明形状很简单：
```` css
.element {
	shape-outside: circle(); /* content will flow around the circle defined on the element */
}
````
或者
```` css
.element {
	shape-outside: url(path/to/image-with-shape.png);
}
````
然而还需要两个条件：
1. 元素必须是浮动的。
2. 元素必须有内在维度（宽高）。
所以例子如下：
```` css
.element {
	float: left;
	height: 10em;
	width: 15em;
	shape-outside: circle();
}
````
## A Shape's reference box
CSS Shape 是在参考盒中定义和创建的，用于在元素上绘制形状。除了元素的高度和宽度，元素的盒模型--margin box,content box,padding box及border box也用于作为指定元素形状边界的参考。

默认，margin box用于作为参考，所以如果一个元素在底部有外边距，你在元素上定义的形状将触及margin 区域的边界，而不是border区域。如果你想要用其它的box值，你可以结合shape function指定shape属性：
```` css
shape-outside: circle(250px at 50% 50%) padding-box;
````
## Defining Shapes using shape functions
<p data-height="265" data-theme-id="dark" data-slug-hash="KZjKEq" data-default-tab="result" data-user="JOHNNYGUAN" data-embed-version="2" data-pen-title="KZjKEq" class="codepen">See the Pen <a href="https://codepen.io/JOHNNYGUAN/pen/KZjKEq/">KZjKEq</a> by JOHNNY (<a href="https://codepen.io/JOHNNYGUAN">@JOHNNYGUAN</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## Defining a shape using an image
使用图像作为形状，这个图像需要有alpha通道，从而浏览器可以提取形状。
形状是由alpha值大于某一阈值的像素构成的。阈值默认是0.0（完全透明），你也可以通过*shape-image-shreshold*属性进行更改。

使用*url()*值指定*shape-outside*属性，我们可以将内容围绕在该形状周围。

<div class="demo">
    <div style="width:64px; height:64px; float:left; background:blue; shape-outside: url(hot.png); mask-image:url(hot.png);-webkit-mask-image:url(hot.png)"></div><p style="margin: 0;">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Harum itaque nam blanditiis eveniet enim eligendi quae adipisci?</p><p style="margin: 0;">Assumenda blanditiis voluptas tempore porro quibusdam beatae deleniti quod asperiores sapiente dolorem error! Quo nam quasi soluta reprehenderit laudantium optio ipsam ducimus consequatur enim fuga quibusdam mollitia nesciunt modi.</p>
</div>
