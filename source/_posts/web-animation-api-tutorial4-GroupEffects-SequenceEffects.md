---
title: 'web-animation-api tutorial4: GroupEffects & SequenceEffects'
date: 2018-01-23 09:23:34
tags:
---
由http://danielcwilson.com/blog/2015/09/animations-part-4/  翻译

我们继续讨论Web Animations API下的 *multiple animations*，实现群组和队列效果。

## KeyframeEffects
一个KeyframeEffect接收三个参数：需要做动画的元素，keyframe数组以及时间选项。这个新的对象本质上是一个单独动画的蓝图，但我们讨论群组及队列动画的方式时，我们会接触它。它不会启动一个动画，它只是定义一个动画。
```` javascript
var elem = document.getElementById('toAnimate');
var timings = {
  duration: 1000,
  fill: 'both'
}
var keyframes = [
  { opacity: 1 }.
  { opacity: 0 }
];

var effect = new KeyframeEffect(elem, keyframes, timings);
````

## GroupEffects
虽然没有实现并且在Level1 spec也找不到，polyfill提供一种组合动画并将它们一起播放的方式。*GroupEffect*（即将在Level2 spec出现）将一个或更多的*KeyframeEffect*组合，用以同时播放。

*GroupEffect*接收效果参数（代表多个动画的*KeyframeEffect*数组）。一旦定义，我们可以播放一组动画。

```` javascript
var elem = document.getElementById('toAnimate');
var elem2 = document.getElementById('toAnimate2');
var timings = {
  duration: 1000
}
var keyframes = [
  { opacity: 1 }.
  { opacity: 0 }
];

var kEffects = [
  new KeyframeEffect(elem, keyframes, timings),
  new KeyframeEffect(elem2, keyframes, timings)
];
var group = new GroupEffect(kEffects);
document.timeline.play(group);
````

## SequenceEffects
与*GroupEffect*类似，*SequenceEffect*可以将动画一个接一个播放。你也可以一起使用*GroupEffect*和*SequenceEffect*。
```` javascript
var sequence = new SequenceEffect(kEffects);
document.timeline.play(sequence);
````
## 创建动画的另一种方式
火狐支持另一种方式：*Animation*构造函数。回顾我们之前的方式：
```` javascript
var elem = document.getElementById('toAnimate');
var timings = {
  duration: 1000,
  fill: 'both'
}
var keyframes = [
  { opacity: 1 }.
  { opacity: 0 }
];

elem.animate(keyframes, timings);
````
使用同样的变量，下面的代码与之等价
```` javascript
var kEffect = new KeyframeEffect(elem, keyframes, timings);
var player = new Animation(kEffect, elem.ownerDocument.timeline);
player.play();


//MDN查找代码如下
var cats = document.querySelectorAll('.sharedTimelineCat');
cats = Array.prototype.slice.call(cats);

var sharedTimeline = new DocumentTimeline({ originTime: 500 });

cats.forEach(function(cat) { 
  var catKeyframes = new KeyframeEffect(cat, keyframes, timing);
  var catAnimation = new Animation(catKeyframes, sharedTimeline);
  catAnimation.play(); 
});
````