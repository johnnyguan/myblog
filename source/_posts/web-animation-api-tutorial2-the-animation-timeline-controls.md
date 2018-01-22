---
title: 'web-animation-api tutorial2: the animation & timeline controls'
date: 2018-01-22 18:49:09
tags:
---
由http://danielcwilson.com/blog/2015/07/animations-part-2/  翻译
现在我们理解了如何使用Web Animations API，我们再讨论一下状态、控制、回调及时间线。

## 动画播放状态和控制
当调用*element.animate()*时，会返回一个*Animation*对象，动画随机开始播放。为了解动画的当前状态，你可以查看只读属性*playState*，它会返回5个字符串之一。我们也能够通过调用4个方法之一来修改动画的当前状态：
```` javascript
var player = element.animate(/* ... */);
console.log(player.playState); //"running"

player.pause(); //"paused"
player.play();  //"running"
player.cancel(); //"idle"... jump to original state
player.finish(); //"finished"...jump to end state
````

除了*running,paused,idle*和*finished*的播放状态，还定义了*pending*状态，这会在播放状态或暂停状态未决时发生。

## 播放速率
通过*playbackRate*属性来改变播放速率。
```` javascript
var player = element.animate(/* ... */);
console.log(player.playbackRate); //1

player.playbackRate = 2; //double speed, can also be decimal to slow it down.
````

## 完成回调
使用CSS过渡，当过渡结束时会触发事件。类似地，*Animation*会在动画完成或者调用finish()。注意根据规范，无限次循环的动画集是不能终止的，播放率也不能设为0。也有*oncancel*句柄，以及*Animation*完成时使用Promise的选项。

## 时间线
每个*Animation*暴露出两个读/写时间相关的属性--*currentTime*和*startTime*。现在我们关注前者。

*currentTime*返回动画目前的毫秒数。最大值是*delay + (duration * iterations)*，所以无限循环不会有最大值。

```` javascript
var player = element.animate([
  {opacity: 1}, {opacity: 0}
], {
  duration: 1000,
  delay: 500,
  iterations: 3
});

player.onfinish = function() {
  console.log(player.currentTime); // 3500
};
````
播放速率会影响到时间线进展的快慢。如果将播放速率设为10，最大currentTime不变，但是整个时间线会缩短为1/10。

由于*currentTime*是读/写的，我们可以使用这个跳跃到时间线的某个点。它也可以用来同步两个动画。

## 另一个选项：reverse()
你也可以使用*reverse()*来反转一个动画，这与*play()*相似，但是会逆时间线发展。当动画完成时*currentTime*会是0。