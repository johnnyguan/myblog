---
title: 'web-animation-api tutorial1: creating a basic animation'
date: 2018-01-22 13:49:56
tags:
---
由http://danielcwilson.com/blog/2015/07/animations-part-1/翻译

我们已经大致了解了Web Animation API，现在我们深入学习一下真实规范。

WAAPI让你能够比使用CSS动画做更多的控制，我们首先使用这个API做一个基本动画。

## 构建关键帧动画
如果你对CSS过渡/动画熟悉，它看起来会很类似。
``` javascript
var player = document.getElementById('toAnimate').animate([
    { transform: 'scale(1)', opacity: 1, offset: 0 },
    { transform: 'scale(.5)', opacity: .5, offset: .3 },
    { transform: 'scale(.667)', opacity: .667, offset: .7875 },
    { transform: 'scale(.6)', opacity: .6, offset: 1 }
  ], {
    duration: 700, //milliseconds
    easing: 'ease-in-out', //'linear', a bezier curve, etc.
    delay: 10, //milliseconds
    iterations: Infinity, //or a number
    direction: 'alternate', //'normal', 'reverse', etc.
    fill: 'forwards' //'backwards', 'both', 'none', 'auto'
  });
```
为了对比起见，有一个同等的CSS关键帧动画。
```` javascript
@keyframes emphasis {
  0% {
    transform: scale(1); 
    opacity: 1; 
  }
  30% {
    transform: scale(.5); 
    opacity: .5; 
  }
  78.75% {
    transform: scale(.667); 
    opacity: .667; 
  }
  100% {
    transform: scale(.6);
    opacity: .6; 
  }
}
#toAnimate {
  animation: emphasis 700ms ease-in-out 10ms infinite alternate forwards;
}
````

我们将这个动画分解并对各个部分进行解释。
```` javascript
var player = document.getElementById('toAnimate').animate() 
````
这个动画会返回一个*Animation*对象，我们之后会用它做一些有趣的事，因而要用一个变量将其保存。我们找到想要做动画的元素（这里用*document.getElementById*获取），调用*animate*函数。这个函数是新加进规范的，所以你需要测试支持性，或者引入polyfill。

*animate*函数接收两个参数，一个关键帧效果(*KeyframeEffect*)数组，一个动画效果时间属性（*AnimationEffectTimingProperties*）选项。从本质上来看，第一个参数映射为你想要再CSS@keyframes中放置的参数，第二个参数则是你想通过*animation-*属性指定的CSS规则。这里的关键益处在于我们能够使用变量，或者重复使用预先定义的*KeyframeEffect*，而在CSS中，我们会受限于我们声明的CSS值。

```` javascript
var player = document.getElementById('toAnimate').animate([
    { transform: 'scale(1)', opacity: 1 },
    { transform: 'scale(.5)', opacity: .5 },
    { transform: 'scale(.667)', opacity: .667 },
    { transform: 'scale(.6)', opacity: .6 }
]);
````
对于每个*KeyframeEffect*，我们将CSS中的offset值变为0-1之间的小数offset值。它是可选的，如果你不指定，它们会均匀分布。你也可以指定*easing*属性，效果与CSS中的*animmation-timing-function*一致。其它*KeyframeEffect*中的属性是animate中的属性。每个属性的值应该与你在javascript中使用*element.style*指定保持一致，所以*opacity*是数字，*transform*是字符串。

```` javascript
var player = document.getElementById('toAnimate').animate([], {
    duration: 700, //milliseconds
    easing: 'ease-in-out', //'linear', a bezier curve, etc.
    delay: 10, //milliseconds
    iterations: Infinity, //or a number
    direction: 'alternate', //'normal', 'reverse', etc.
    fill: 'forwards' //'backwards', 'both', 'none', 'auto'
});
````
<p data-height="265" data-theme-id="dark" data-slug-hash="eyXdoZ" data-default-tab="css,result" data-user="JOHNNYGUAN" data-embed-version="2" data-pen-title="animation" class="codepen">See the Pen <a href="https://codepen.io/JOHNNYGUAN/pen/eyXdoZ/">animation</a> by JOHNNY (<a href="https://codepen.io/JOHNNYGUAN">@JOHNNYGUAN</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>