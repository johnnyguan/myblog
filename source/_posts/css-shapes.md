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
