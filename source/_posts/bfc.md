---
title: bfc
date: 2018-02-09 15:18:43
tags:
---
## 概念
FC(Formatting Context)格式化上下文，是CSS2.1规范中的一个概念。它是页面中的一块渲染区域，并且由一套渲染规则，它决定**子元素**将如何定位，以及和**其它元素**的关系及相互作用。

BFC(Block Formatting Context)块级格式化上下文。
具有BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器没有的特性。
通俗来说可以把BFC理解为封闭的大箱子，箱子内部元素无论如何翻江倒海，都不会影响到外部。

## 触发BFC
只要元素满足下面任一条件即可触发BFC特性：
- body根元素
- 浮动元素：float除none以外的值
- 绝对定位元素：position(absolute、fixed)
- display为inline-block、table-cell、flex
- overflow除了visible以外的值(hidden、auto、scroll)

## BFC特性及应用
1. BFC可以包含浮动的元素（清除浮动）
<p data-height="521" data-theme-id="dark" data-slug-hash="VQPNZQ" data-default-tab="result" data-user="JOHNNYGUAN" data-embed-version="2" data-pen-title="float" class="codepen">See the Pen <a href="https://codepen.io/JOHNNYGUAN/pen/VQPNZQ/">float</a> by JOHNNY (<a href="https://codepen.io/JOHNNYGUAN">@JOHNNYGUAN</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

2. BFC可以阻止元素被浮动元素覆盖
<p data-height="904" data-theme-id="dark" data-slug-hash="NydmxQ" data-default-tab="result" data-user="JOHNNYGUAN" data-embed-version="2" data-pen-title="float_overlap" class="codepen">See the Pen <a href="https://codepen.io/JOHNNYGUAN/pen/NydmxQ/">float_overlap</a> by JOHNNY (<a href="https://codepen.io/JOHNNYGUAN">@JOHNNYGUAN</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

**下图中形成bfc的元素可以防止浮动元素将其覆盖**
