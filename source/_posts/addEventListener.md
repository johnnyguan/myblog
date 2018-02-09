---
title: addEventListener
date: 2018-02-07 14:29:54
tags:
---
参考 https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener

addEventListener是W3C DOM规范中提供的注册事件监听器的方法。

使用方法
```` javascript
target.addEventListener(type, listener, options);

target.addEventListener(type, listener ,{capture: Boolean, bubbling: Boolean, once: Boolean});

target.addEventListener(type, listener, useCapture);
````

type和listener没啥特别的，这个方法我之前用的最多的是第三种形式，查看MDN才发现第三个参数还可以是对象。来看一下这个对象。
- capture:  Boolean，表示 listener 会在该类型的事件捕获阶段传播到该 EventTarget 时触发。
- once:  Boolean，表示 listener 在添加之后最多只调用一次。如果是 true， listener 会在其被调用之后自动移除。
- passive: Boolean，表示 listener 永远不会调用 preventDefault()。如果 listener 仍然调用了这个函数，客户端将会忽略它并抛出一个控制台警告。

*capture*与*useCapture*的效果一样。
使用*once*在调用事件处理函数之后会自动移除该事件监听，即只触发一次，效果与jQuery的$(dom).one(...)一致。
*passive*则明确表示不会调用preventDefault()，如果依然调用，则被忽视。可以使用该参数改善滚屏性能。
```` javascript
var elem = document.getElementById('elem'); 
elem.addEventListener('touchmove', function listener() { /* do something */ }, { passive: true });
````

检测*passive*可以使用如下代码
```` javascript
var passiveSupported = false;

try {
  var options = Object.defineProperty({}, "passive", {
    get: function() {
      passiveSupported = true;
    }
  });

  window.addEventListener("test", null, options);
} catch(err) {}
````

另外，**对于相同的事件处理函数**,addEventListener**只会绑定一次**
```` javascript
ele.addEventListener('click',handler,false);
ele.addEventListener('click',handler,false);//只会绑一次

ele.addEventListener('click',function(){
    ...
},false);
ele.addEventListener('click',function(){
    ...
},false);//两个匿名函数即使内容一样，也是两个不同的事件处理函数
````