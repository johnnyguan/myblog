---
title: collapse margin
date: 2018-02-09 14:48:09
tags:
---
`有时候明明是在子元素上加margin-top，但是页面上显示的却是在父元素上加了margin-top。这是什么原因呢？`
<p data-height="335" data-theme-id="dark" data-slug-hash="rJjPoP" data-default-tab="result" data-user="JOHNNYGUAN" data-embed-version="2" data-pen-title="margin-top" class="codepen">See the Pen <a href="https://codepen.io/JOHNNYGUAN/pen/rJjPoP/">margin-top</a> by JOHNNY (<a href="https://codepen.io/JOHNNYGUAN">@JOHNNYGUAN</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
这个问题是CSS2.1的盒模型中规定的内容——Collapsing margins：

In this specification, the expression collapsing margins means that adjoining margins (no non-empty content, padding or border areas or clearance separate them) of two or more boxes (which may be next to one another or nested) combine to form a single margin. 所有毗邻的两个或更多盒元素的margin将会合并为一个margin共享之。毗邻的定义为：**同级或者嵌套的盒元素，并且它们之间没有非空内容、Padding或Border分隔**。

也就是说父元素没有border、padding且父子元素之间没有非空内容时，父子元素的margin会合并，最终体现为父元素的margin。