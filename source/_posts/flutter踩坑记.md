---
title: flutter踩坑记
date: 2018-11-01 13:58:17
tags:
---
近期研究flutter，遇到不少坑，现记录在本文中，以供参考。
### 嵌套ListView ###
在做可滚动的列表时，会使用到ListView，而由于布局，常常会出现嵌套的ListView，本人碰到两种情况：

1. 控制台报一大堆错
2. 屏幕并不可以滚动

遇到这两种情况，可以考虑加上`shrinkWrap:true`及`physics: ClampingScrollPhysics()`。

### 底部空间不够 ###
在有表单的页面，当输入框弹出时，出现**BOTTOM OVERFLOWED BY 20 PIXEL**字样，并伴有黄黑色条纹，此时应考虑在布局上使用`ListView`。

### boxshadow要点 ###
在使用`BoxDecoration`加入boxshadow时，一定要同时设背景色`color`，否则阴影会模糊整个盒子。