---
title: web animations api（译）
date: 2018-01-22 10:36:38
tags:
---

由http://danielcwilson.com/blog/2015/07/animations-intro/ 翻译

# Let's talk about the Web Animations API

在2014年夏天，谷歌在网上通过Polymer宣告Material design..使用了即将来临的Web Animations API标准的polyfill。

我从未听过这个API，但是我被吸引了，尤其是因为它讨论了MotionPath效果。它还没有完成，但是它提供一种统一CSS、JS和SVG方式来做动画的目的吸引了我。一年后，谷歌和火狐开始实现该标准，polyfill的进程也已经稳定，是时候认真地看待它了。

但是很少有人讨论WAAPI！我希望现在通过写一系列文章，突出它在浏览器中的特色，探索我们为什么想要这个API，搞清楚它们的细微差别。

## 什么是Web Animation API
我们通过弄清它是什么及它想要实现什么来开始这次探索。

动画在过去5年进展很好，有很好的CSS支持以及对javascript的支持。但是在它们提供很多好处的同时，仍然有大量的缺点。
- CSS拥有对于平滑过渡的硬件加速，并且是内置于浏览器中的。但是它的规则是在CSS中声明，需要很费劲的使用javascript来动态改变值。
- *requestAnimationFrame*拥有很好的支持，会让浏览器优化何时开始动画，但它仍然可能在有大量其它js运行的时候挂起。它也需要更多的数学来倒计时。
- *setInterval*将很多开发者引入到动画中，但它是不精确的，也会导致不流畅的动画。
- *jQuery.animate()*将其它一些开发者带入动画，但通常会有性能问题。
- 诸如Velocity和GreenSock(GSAP)提升了js性能，并且在很多场景下测试显示为最佳。但是，它们需要维护并且引入外部库。

通常来说，我们喜欢浏览器尽可能支持并且由浏览器进行优化。浏览器现在有*document.querySelector*，因为我们看到jQuery提供这种选择DOM元素的方式。所以库中的功能被迁移到浏览器中。理想情况，我们能够将尽可能多的动画控制放在浏览器层面。这些库就可以专注于新特性，然后良性循环。

Web Animation API致力于此。它旨在带来CSS性能方面的能力，加上js的便利和灵活性。

## 让我们加一些新东西来解决问题
在前一份工作，我们收到一份邮件，说他们知道我们在公司事务方面有太多的地方需要查看 -- email，办公室监视器，Yammer， Google Chat及intranet/wiki。为解决这个问题，他们加了一个博客。

当我第一次听到Web Animation API的时候，我的想法和我听到我公司要加博客时一样 -- 它只会让事情变得更糟。这个博客没有中心化任何事物，它仅仅是额外增加了我们要查看新闻的地方，然后它死掉了。

但是这个感觉是不一样的。规范展示了它的关注点。它不是为了替代已有的行为，而是要统一。语法类似CSS，但是增加了变量、控制和完成回调的选项。