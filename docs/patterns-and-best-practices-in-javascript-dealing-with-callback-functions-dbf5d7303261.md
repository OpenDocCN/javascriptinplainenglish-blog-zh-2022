# JavaScript 中的模式和最佳实践:处理回调函数

> 原文：<https://javascript.plainenglish.io/patterns-and-best-practices-in-javascript-dealing-with-callback-functions-dbf5d7303261?source=collection_archive---------4----------------------->

## 与任何其他编程语言一样，JavaScript 有许多最佳实践和相关的不良实践。由于其动态特性，JavaScript 也有各种各样的陷阱。

![](img/cc13be0fc8a5659ba5e201ef796d6e45.png)

Photo by [Carl Heyerdahl](https://unsplash.com/@carlheyerdahl?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) / [Unsplash](https://unsplash.com/s/photos/technology-software-deve?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

与任何其他编程语言一样，JavaScript 有许多最佳实践和相关的不良实践。由于其动态特性，JavaScript 也有各种各样的陷阱。

回调函数是作为参数传递给其他函数并由它们调用的函数。它们是异步 JavaScript 开发中常见的设计模式。这种设计模式的基本(还不是最佳)结构如下:

`doStuff()`函数需要一个函数作为参数，并在特定的时间点调用它:

# 检查回调函数类型

由于 JavaScript 的弱类型，一个期望(回调)函数作为参数的函数原则上也可以被传递任何其他值(或者根本没有值)。但是，调用这个假定的函数不可避免地会导致类型错误(“回调不是函数”)。根据上面的示例，以下调用是可能的，但不可取:

因此，首先检查函数内部回调参数的类型并确保它确实是一个函数是很重要的。这可以通过使用`typeof`操作符来实现，如下面的清单所示。如果它为所传递的参数返回值“function ”,那么它就是一个函数，没有任何东西会妨碍它的调用:

如果在一个函数中有几个地方可以调用回调函数，那么这个检查必须在所有这些地方之前进行:

如果在函数的开头执行检查，并且在回调参数不是函数的情况下，简单地用一个匿名的空函数重新定义它，就可以避免这种情况，如下所示。这个简单而有效的技巧一下子保护了对回调函数的所有以下调用:

在条件操作符的帮助下，整个事情甚至可以简化为一行代码:

# 回调函数的参数

因为回调函数是异步调用的，既不能提供直接返回值也不能抛出错误，所以至少应该为这两种情况提供适当的参数:

1.  一个参数包含关于在错误事件中发生的错误的信息，
2.  一个通常包含异步计算结果的参数。

即使这两个参数的顺序原则上并不重要，但它已经成为一种约定——尤其是在开发 Node.js 模块时——将错误列为第一个参数，将结果列为第二个参数(如果没有错误，第一个参数对应零)。

您可以在回调函数中使用简单的 if 查询来确定是否发生了错误:

# 回叫呼叫的返回

在某些情况下，调用前面例子中显示的回调函数会导致意外的程序行为。例如，在倒数第二个清单中，回调函数被调用两次，以防出现错误。

下面是代码:

这里的问题是，try-catch 块之后的代码总是会被调用。即使 catch 块先前由于错误而被跳转，并且在那里调用了回调函数。这是一个你在阅读源代码时很容易忽略的事实。因此，您应该在每次调用回调函数之前放置一个“return ”,它直接跳出调用函数。

当然，这样做的先决条件是调用函数的结构是相应的，并且回调函数的调用总是表示函数的结束。

例如，下面的代码片段显示了错误的做法:

# 回调函数的执行上下文

当通过`this`将函数作为访问执行上下文的回调参数传递时，需要特别小心。在这种情况下，您必须利用`bind()`函数并使用它来创建一个绑定到所需执行上下文的新函数。

然后，这个新函数作为回调参数传递:

# 结论

使用回调函数时，应该考虑几个最佳实践，包括类型检查、回调参数的顺序、调用回调函数一次以及设置执行上下文。

关于异步编程是使用承诺、生成器函数还是 async/await 组合来代替回调函数的基本问题将在下面的文章中讨论。

关于 JavaScript 中回调函数的解释到此结束。请随时在我的[个人简讯/博客](https://www.paulsblog.dev)、 [LinkedIn](https://www.linkedin.com/in/paulknulst/) 、 [Twitter](https://twitter.com/paulknulst) 和 [GitHub](https://github.com/paulknulst) 上与我联系。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*