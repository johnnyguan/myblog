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
