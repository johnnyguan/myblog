---
title: web-animations-api-tutorial3-multiple-animations
date: 2018-01-22 23:17:07
tags:
---
由http://danielcwilson.com/blog/2015/08/animations-part-3/  翻译

我们讨论多个动画。
## 每个元素上有多个动画
<p data-height="265" data-theme-id="0" data-slug-hash="dJrmJy" data-default-tab="js,result" data-user="JOHNNYGUAN" data-embed-version="2" data-pen-title="multi-animation" class="codepen">See the Pen <a href="https://codepen.io/JOHNNYGUAN/pen/dJrmJy/">multi-animation</a> by JOHNNY (<a href="https://codepen.io/JOHNNYGUAN">@JOHNNYGUAN</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

在这个例子中，每个矩形应用了三个动画（改变transform、opacity和color）。你可以在一个元素上多次调用*animate()*，这与CSS上使用多个动画是类似的。

使用CSS时：
```` javascript
#toAnimate {
  animation: pulse 1s, activate 3000ms, have-fun-with-it 2.5s;
}
@keyframes pulse { /* ... */ }
@keyframes activate { /* ... */ }
@keyframes have-fun-with-it { /* ... */ }
````
使用Web Animations API
```` javascript
var animated = document.getElementById('toAnimate');
var pulseKeyframes, //defined the keyframes here.
    activateKeyframes,
    haveFunKeyframes;
var pulse = animated.animate(pulseKeyframes, 1000); //the second parameter as a number is a valid shorthand for duration
var activate = animated.animate(activateKeyframes, 3000);
var haveFunWithIt = animated.animate(haveFunKeyframes, 2500);
````
使用Web Animations API时，创造了三个*Animation*对象，它们可以被暂停，播放，完成，取消以及通过时间线或播放速率进行操作。

## Get the AnimationS,Get Them All

当你在调用*animate()*时没有保存*Animation*引用时，应该做什么？
规范规定在document上有一个*getAnimations()*方法。在最新版本的规范，这个方法直接在document对象上，火狐48+也是这么实现的。但是Chrome52以及polyfill(v2.2.0)，是根据旧规范实现的，这个方法在timeline对象上。

```` javascript
//If including the polyfill you can use the following
var animations = document.getAnimations ? document.getAnimations() : document.timeline.getAnimations();
//returns array of all active (not finished and not canceled) animations
````

