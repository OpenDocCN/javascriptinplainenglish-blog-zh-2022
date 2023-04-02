# JavaScript 中“let”和“var”的 4 个区别

> 原文：<https://javascript.plainenglish.io/4-difference-between-let-and-var-in-js-621cc77d60cb?source=collection_archive---------19----------------------->

## 每个 JavaScript 开发者都应该知道的“let”和“var”的 4 个区别

![](img/6321faec34aeccfab6aa89094ea0a08a.png)

Credit due to Andrea Piacquadio

在 JavaScript 开发中，我们经常使用`var`和`let`关键字，但是有些开发人员并不是很清楚这两者的区别。这篇文章详细解释了它们的区别，你将能够完全区分这些关键词！

## **1。范围:**

`let`和`var`的范围很不一样。`var`关键字的作用域是当前函数体，而`let`关键字的作用域在它的括号内更小。简单地说，这意味着`var`变量在整个函数中都是可见的，而`let`变量只对封闭的`{}`可见。请参见下面的示例:

在示例中，我们定义了`a,b,c,d` 4 个变量。由于`a,c`是通过`var`关键字定义的，我们将知道即使`c`是在右括号中定义的，它们在整个函数中都是可访问的。另一方面，由于`d`是由`let`定义的，并且是在结束括号内定义的，如果我们试图在结束上下文之外访问它，我们会得到一个错误，因为 JavaScript 编译器不会看到它是在`{}`之外定义的。很简单，不是吗？这种差异直接导致了一些后果:定义变量时要小心:如果你不希望这个变量存在于`block`之外，比如`for(let i = 0; ..)`，你最好不要使用`var`。

## 2.**吊装:**

你们中的一些人可能对上面的例子感到疑惑:你说`a,c`在整个函数中都有定义。那么如果你试图在括号`{}`中定义`c`之前调用它会发生什么？好问题，让我们看看会发生什么:

如你所见，将会是`undefined`。这实际上是`let`和`var`的一大区别。既然带有`var`的东西对整个函数块都是可见的，那么在声明之前`var`的值是多少呢？答案是 JavaScript 将为变量赋值`undefined`，直到它被声明。这叫吊装。另一方面，如果我们试图访问一个在声明前通过`let`定义的变量，JavaScript 会抱怨:

如你所见，编译器会抛出一个`ReferenceError`。

## 3.**全局状态:**

正如我们在第一节中暗示的，全局状态有些模糊。我们可以通过`let`和`var`在函数之外定义变量。然而，不同的声明导致不同的结果。用`var`定义的变量是全局对象属性的一部分，可以作为`glocalThis`访问，而通过`let`定义的变量则不是这样。注意`globalThis`可以有不同形式，这取决于您执行 JavaScript 的位置。它可以是您的 JavaScript 程序中的关键字，如`self`、`window`或`global`。因此，为了避免混淆，我不会在这里放一个代码片段，但是您已经明白了。

## 4.重新声明:

最后，`var`和`let`有一个很大的区别。在`var`中，我们可能会使用相同的名称重新声明变量，而在`let`中不会发生这种情况，否则将会抛出错误。请参见以下代码片段:

在上面的例子中，在`a`上有三个使用`var`的声明，它运行得很好，但是只要我们声明两个`b`，JavaScript 就会像你看到的那样抱怨。

这就是 JavaScript 中关键字`let`和`var`的 4 个不同之处。请注意它们区别，并在定义变量时小心谨慎。尤其是，仔细考虑你希望你的变量在什么范围内。快乐学习，快乐编码！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*