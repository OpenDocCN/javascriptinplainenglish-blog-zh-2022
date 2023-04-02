# 什么是 JavaScript 闭包？

> 原文：<https://javascript.plainenglish.io/what-are-javascript-closures-d27a5ed7a79f?source=collection_archive---------16----------------------->

![](img/f18cdeab9681886453603ab310ead7f9.png)

Photo by [Christin Hume](https://unsplash.com/@christinhumephoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在编程的世界里，闭包是那些似乎会给初学者带来很多困惑的事物之一。但是一旦你理解了它们，它们就是你编程武库中的一个强大工具。在这篇博文中，我们将讨论什么是闭包，以及它们在 JavaScript 中是如何工作的。

## 什么是闭包？

简单来说，闭包就是嵌套函数使用外部函数中的变量。内部函数可以访问外部函数中的变量，即使外部函数已经返回。这是可能的，因为当你返回一个函数时，你实际上是在返回对那个函数的引用。即使外部函数不再运行，内部函数仍然可以访问外部作用域中的变量。这可能没有多大意义，所以让我们来看一些例子。

## 闭包的例子

假设我们想写一个函数，它有两个参数并返回这些参数的和。我们可以这样写这个函数:

```
function add(x, y) { return x + y;}
```

现在假设我们想创建一个函数，它总是返回两个数的和，不管这两个数是什么。我们可以通过使用闭包来实现这一点:

```
function makeAdder() { let x = 0; let y = 1; return function() { return x + y; };}let adder = makeAdder();adder(); // returns 1
```

现在我们有了一个函数，加法器，它能记住传递给它的 x 和 y 的值。这是一个闭包的例子。

![](img/907e12850a1c2e6db5165e1dc8f4c837.png)

Photo by [Surface](https://unsplash.com/@surface?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 闭包在 JavaScript 中的实际应用

闭包通常用在 JavaScript 中，比如创建需要记住创建环境信息的函数。例如，当您创建一个事件侦听器时，事件发生时调用的函数需要记住它附加到了什么元素。这可以使用闭包来完成:

```
document.getElementById(‘some-element’).addEventListener(‘click’, function() {// this function has access to someElement});
```

在此示例中，传递给 addEventListener 的函数可以访问 someElement，即使 someElement 没有显式传递给该函数。

闭包的另一个常见用途是创建需要私有变量的函数。这可以通过在另一个函数中创建闭包来实现:

```
function createCounter() { let count = 0; return function() { count++; return count; };}let counter = createCounter();console.log(counter()); // 1console.log(counter()); // 2counter.count; // undefined
```

正如您所看到的，createCounter 返回的函数可以访问变量 count，即使该变量没有显式地传递给函数。然而，状态是私有的，我们不能访问 count 变量。

这是对闭包的简单介绍，以及它们在 JavaScript 中是如何工作的。如果您是闭包的新手，我建议您阅读更多关于闭包的内容，并做一些练习。通过一些理解和实践，闭包可以成为您编程武库中的一个强大工具。编码快乐！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*