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