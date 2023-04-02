# JavaScript 中函数声明和函数表达式的区别

> 原文：<https://javascript.plainenglish.io/the-difference-between-function-declaration-function-expression-in-javascript-3732a6113787?source=collection_archive---------6----------------------->

## 了解 JavaScript 中何时使用函数声明和函数表达式。

![](img/09c9086da2fc1bf41ab7c0b952a77d13.png)

Photo by [Brooke Cagle](https://unsplash.com/@brookecagle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，创建函数有两种方式:函数声明和函数表达式。函数声明用关键字“Function”编写，而函数表达式用变量关键字定义，并将函数存储在变量中。在这篇博文中，我们将讨论这两种类型的函数之间的区别，以及何时应该使用每一种函数。

## 函数声明

函数声明是声明函数的传统方法。函数声明的结构如下:

```
function myFunction() { // do something}
```

如您所见，function 关键字用于创建函数声明。函数名(在本例中为“myFunction”)后跟一组括号。花括号内的代码是函数的主体，这是您编写调用函数时将执行的代码的地方。

## 函数表达式

将函数赋给变量时，会创建一个函数表达式。函数表达式的结构如下:

```
let myFunction = function() { // do something}
```

如您所见，该函数被赋给了变量“myFunction”。这个函数没有名字，所以它是匿名的。由于 JavaScript 的一流函数支持，我们能够将函数赋给变量。JavaScript 中的函数可以像其他变量一样对待，这就是我们创建函数表达式的原因。

花括号内的代码是函数的主体，这是您编写调用函数时将执行的代码的地方。

![](img/f0a6a8b0fb14d78d57ba2dc656f36a47.png)

Photo by [Clay Banks](https://unsplash.com/@claybanks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 主要差异

函数声明和函数表达式之间有几个关键区别:

*   函数声明是悬挂的，而函数表达式不是。这意味着函数声明在定义之前可以被调用，而函数表达式则不能。
*   函数声明必须有名字，而函数表达式没有。这是因为函数表达式存储在变量中。

## 何时使用每一个

那么，什么时候应该使用函数声明，什么时候应该使用函数表达式呢？使用函数表达式是很好的实践，因为它可以产生可维护的代码。这样做的原因是函数表达式没有被提升，所以你可以确定函数在定义之前不会被调用，这样更容易调试。此外，函数表达式允许您创建匿名函数，这在某些情况下很有用。

但是，在某些情况下，您可能需要使用函数声明。一个例子是当你需要递归调用一个函数的时候。因为函数声明是提升的，所以在定义之前就可以调用。

当您希望函数在整个代码中都可用时，应该使用函数声明。当您想要创建匿名函数或者想要控制函数的执行时间时，应该使用函数表达式。

我希望这篇文章能消除你的任何困惑！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**