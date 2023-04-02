# 一级函数(JavaScript)

> 原文：<https://javascript.plainenglish.io/first-class-functions-90a2fc5176e9?source=collection_archive---------9----------------------->

![](img/4cc2222092b077547fe15a52103c674c.png)

The above image is created by Divyojyoti Ghosh(me) on [www.canva.com](http://www.canva.com/) using different elements available for making designs.

一级函数概念是 JavaScript 中的一个基本概念，也是 JavaScript 区别于其他编程语言的原因之一。

在 JavaScript 中，函数被视为一等公民，即函数被视为任何其他值。由于 JavaScript 中的每个值都有一个数据类型(在我以前关于 JavaScript 中的[数据类型和运算符的一篇文章中讨论过)，函数也有一个数据类型，它的数据类型是“ **function** ”，但实际上，它是另一种类型的**对象**。](https://divyosmiley9.medium.com/datatypes-and-operators-in-javascript-49229b81ef56)

Retrieving the Datatype of a function

像 JavaScript 中的其他值一样，函数也可以赋给任何对象的变量或属性。下面的代码片段可以作为一个例子，像 JavaScript 中的任何其他值一样，将函数分配给变量或属性。

Assigning functions to variables and properties.

`multiplier`变量存储一个接受两个输入并返回其乘积作为输出的函数，而`calculator`变量存储一个具有不同属性的对象，其中两个属性是函数。

此外，我们还可以将函数作为参数传递给其他函数，这与值的工作方式类似。addEventListener 函数经常使用函数的这个属性。我们将一个处理函数传递给 addEventListener 函数，它在事件发生时调用该处理函数(作为另一个参数传递)，下面的代码片段是相同的示例

Passing function as an argument to another function

除此之外，我们还可以从函数中返回函数，就像我们从函数中返回值一样。下面的代码片段可以作为一个例子

1.  在上面的代码片段中，第 8 行调用函数`sample_function`，并将返回值保存到`returned_function`变量中。
2.  `sample_function`打印`"This is the initial function"`，然后返回另一个保存到`returned_function`变量的函数。
3.  当第 10 行被执行时，`returned_function`变量中保存的返回函数被调用，打印出`"i am being returned"`。

除了所有这些属性，JavaScript function 的另一个特性是，我们可以像调用对象值一样调用 function 上的方法。任何函数都可以调用`call()`、`apply()`和`bind()`方法。下面的代码片段可以很好地说明这一特性—

在上面的代码片段中，`call()`方法在`averageMarks()`函数上被调用，类似于我们在任何对象上调用方法的方式。

## 摘要

Javascript 将函数视为一等公民，这意味着函数只是值。我们可以将函数存储在变量中，将函数作为参数传递给另一个函数，从函数返回函数，还可以对函数调用方法。

## 资源

[](https://www.w3schools.com/js) [## JavaScript 教程

### JavaScript 是世界上最流行的编程语言。JavaScript 是网络的编程语言…

www.w3schools.com](https://www.w3schools.com/js) [](https://www.geeksforgeeks.org/what-is-the-first-class-function-in-javascript/) [## JavaScript 中的第一个类函数是什么？- GeeksforGeeks

### 一级函数:如果一种编程语言中的函数是…

www.geeksforgeeks.org](https://www.geeksforgeeks.org/what-is-the-first-class-function-in-javascript/) [](https://gist.github.com/) [## 发现要点

### GitHub Gist:即时共享代码、笔记和片段。

gist.github.com](https://gist.github.com/) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)**** ***对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。*****