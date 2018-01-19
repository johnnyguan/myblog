---
title: atan与atan2(译 wikipedia)
date: 2018-01-06 13:25:27
tags: [数学]
---

## 概论
很多计算机语言都提供了以*atan2(y,x)*或*arctan2(y,x)*为名的多值反正切函数。这个函数接受两个参数*y*和*x*（不能同时为0，代表*X/Y*平面中除原点外的任意点*(x,y)*）。比例*y/x*为原点到该点的射线与x轴的夹角角*&theta;*。返回的弧度角封闭在区间(-π,π],并且在*y>0*时值为正。

![Graph of atan2(y,x) over y/x](Arctangent2.svg)
<figure class="image-bubble">
    <div class="img-lightbox">
        <div class="overlay"></div>
        <img src="/2018/01/06//atan%E4%B8%8Eatan2/Atan2_argument_sign_graph.svg" alt="Graph of the tangent function from −π to +π with the corresponding signs of y over x" title="" width="450">
    </div>
    <div class="image-caption">Graph of the tangent function from −π to +π with the corresponding signs of y over x</div>
</figure>

## 历史与动机
*atan2*函数首先是在计算机编程语言中引入的，但现在它在科学及工程领域也很常用。它至少可以追溯到**FORTRAN**编程语言，现在可以在很多现代编程语言中找到。其中有C语言的math.h 标准库，Java Math库，.NET的System.Math，Python的math模块等。

接受一个参数的arctangent函数不能直接区分相对方向。例如，从x轴到向量(1,1)的逆时针角，记为 *arctan(1/1)*，为π/4弧度或45°。然而，x轴与向量(-1,-1)之间的夹角，为*arctan(-1/-1)*，但却不是π/4弧度。另外。在求x轴与向量(0,y),y≠0的时候，需要计算*arctan(y/0)*，但是分母不能为0。

相比之下，*arctan2*函数可以通过两个变量*y*和*x*计算出唯一的反正切值。

## 定义与计算
根据标准反正切函数，*arctan2*函数可以表示为
![](f1.svg)
![](f2.svg)
![](f3.svg)
![](f4.svg)


