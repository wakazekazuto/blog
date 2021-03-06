---
title: JavaScript回调函数的实现
date: 2013-02-12
tags: [JavaScript]
categories: 前端
---

在JavaScript中，回调函数的使用非常频繁。特别是在各种Javascript库中，经常在一个函数中使用回调函数，例如jQuery中的each()方法。一年以来，在使用各种有回调函数的函数时，都没有去深究其内部的实现原理真，惭愧。在有米实习时，在读js师兄的代码时，偶然看到他写的一个函数是他自己实现回调函数的，当时感觉很神奇，原来这就是回调函数啊，之后google了很多关于Javascript回调函数的资料，终于大概弄明白回调函数是什么了。以下是自己对回调函数的一些理解。
<!-- more -->

回调函数定义：... 理论一直是我的弱项，定义暂时没法定，以后弄懂再补上，我暂时只懂它的用法orz。

回调函数的基本实现：

``` js
// 声明一个函数，它的参数是一个函数fn
function example(fn)  {
    // 回调前，可以do something
    alert('我是回调前执行的代码');
    // 存在fn则直接用，不存fn在则用函数表达式的方式声明一个
    fn = fn || function() {};
    fn(); //  调用传进来的fn
}
// 调用传进来的fn
function callback() {
    alert('I am callback!')
}
example(callback); // 调用函数a
```

这个例子展示回调函数基本实现方法，实现回调的关键是把一个函数当成另一个参数。当然实践中很少用上面方式去使用回调函数，一般把一个匿名函数传入当成回调函数，这种方法在Javascript中使用非常广泛，下面是一个基本的例子。

``` js
// 声明一个函数，它的参数是一个函数fn
function example(fn) {
// 回调前，可以do something
    alert('我是回调前执行的代码');
    // 存在fn则直接用，不存fn在则用函数表达式的方式声明一个
    fn = fn || function() {};
    fn(); // 调用传进来的fn
}
// 把匿名函数当做参数
example(function()  {
    alert('I am callback!')
});
```

使用匿名函数作为参数，不仅可以极少代码，也让代码更好管理，更加灵活。

任何函数都是可以传入参数的，回调函数一样:

``` js
// 声明一个函数，它的参数是一个函数fn
function example(a, fn)  {
    // 回调前，可以do something
    alert(a);
    // 存在fn则直接用，不存fn在则用函数表达式的方式声明一个
    fn = fn || function() {};
    fn(m); // 调用传进来的fn
}
// 把匿名函数当做参数
var m = 'I am callback!';
example('我是回调前执行的代码',  function(m)  {
    alert(m)
});
```

以上就是Javascript回调函数的实现方法和简单用法，关于回调函数的作用，我的理解是：其实，每个函数的定义都是为了实现某些功能，在一个拥有回调函数的函数中，一般把实现一个功能的通用代码写在回调函数前，其实后也可以，而开发者在回调函数中自定义自己需要的功能。文艺一点，就是回调函数让世界更加多姿多彩。

done。
