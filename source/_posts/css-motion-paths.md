---
title: css motion paths（译）
date: 2018-01-24 09:28:10
tags:
---
由https://codepen.io/danwilson/post/css-motion-paths 翻译
当我开始[深入探索WAAPI](http://danielcwilson.com/blog/2015/07/animations-intro/)，最有趣的是即将支持Motion Paths(运动路径)--沿特定路径进行动画。在这儿的好处是不言而喻的，在没有它的时候，你要沿一条直线进行过渡，需要写一些keyframe，或者需要借助JS库来帮你抽取逻辑。虽然后者使事情变得简单，简单地在已有的CSS(或者WAAPI)动画中加入路径，仍然是很nice的。

Chrome最近声明他们对于[CSS Motion Path module](https://www.w3.org/TR/motion-1/)的[原生支持](https://www.chromestatus.com/features/6190642178818048)

## 我们怎样做到？
在CSS和js中有三个新的*motion*属性，我们可以将其与transitions，CSS keyframe动画或者WAAPI结合。
### MOTION-PATH
首先，*motion-path*定义运动的路径。你可以像在SVG1.1中定义路径一样来定义一条motion-path。
```` 
motion-path: path("M200 200 S 200.5 200.1 348.7 184.4z");
````
也可以接受*fill-rule*作为path中可选的第一个参数。你也可以使用诸如*circle*，*polygon*，*ellipse*和*inset*的基本形状。如果你使用过[CSS Shapes](http://alistapart.com/article/css-shapes-101)，你会对它很熟悉。最后你也可以通过*url()*引用形状。
<p data-height="265" data-theme-id="dark" data-slug-hash="ZGmeRO" data-default-tab="css,result" data-user="danwilson" data-embed-version="2" data-pen-title="CSS Motion Path Spiral" class="codepen">See the Pen <a href="https://codepen.io/danwilson/pen/ZGmeRO/">CSS Motion Path Spiral</a> by Dan Wilson (<a href="https://codepen.io/danwilson">@danwilson</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
### MOTION-OFFSET
我们使用*motion-offset*指定物体出现的位置。它可以是一个double length value或者一个百分比。所以当我们沿路径从起始点运动到终点，我们创建一个从0到100%的动画。使用CSS keyframe:
````
@keyframes path-animation {
  0% { 
    motion-offset: 0;
  }
  100% { 
    motion-offset: '100%';
  }
}
````
使用WAAPI:
````
m.animate([
    { motionOffset: 0 },
    { motionOffset: '100%' }
], 1000);
````
### MOTION-ROTATION
物体面对的方向是由*motion-rotation*属性处理的。目前有4个主要的方式来处理：
- 值"auto"意味着元素会随路径旋转。
- 值"reverse"指元素会随路径旋转，同时加上180度。
- "auto Xdeg"（或者"reverse Xdeg"）会额外旋转一定角度。
- "Xdeg"时物体会始终保持这个角度。
