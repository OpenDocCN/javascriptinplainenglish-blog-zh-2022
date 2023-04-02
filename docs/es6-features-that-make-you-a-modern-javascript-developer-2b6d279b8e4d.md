# 使您成为现代 JavaScript 开发人员的 ES6 特性

> 原文：<https://javascript.plainenglish.io/es6-features-that-make-you-a-modern-javascript-developer-2b6d279b8e4d?source=collection_archive---------6----------------------->

![](img/f35cdd6da1202a429f7722aa03717611.png)

Photo by [Tim van der Kuip](https://unsplash.com/@timmykp?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/software-developer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

ES6 也称为 ECMAScript 2015，是 ECMAScript 语言标准的主要版本之一，它带来了一些令人兴奋的功能。今天，我们将看到它提供的一些优势。

1.  ***let 和 const 关键字***
2.  ***模板文字***
3.  ***多行字符串***
4.  ***箭头功能***
5.  ***承诺***
6.  ***解构***
7.  ***为…的循环***
8.  ***传播算子和休息参数***

让我们一个一个来看看。

# let 和 const 关键字

在过去， ***var*** 关键字被用来定义变量。不过，现在鼓励开发者使用***【let】******const***而不是使用 ***var。***

***let*** 关键字允许用户定义变量，而 ***const*** 帮助定义常量。换句话说，用 ***const*** 声明的变量不能被重新赋值。如果你有一个不应该被意外覆盖的变量，你应该使用 ***const*** 。它会在编译时显示错误。

值得了解的是，为什么不首选使用 var。请参见下面的示例。

仔细看看这两个 for 循环的输出。

变量 ***i*** 在我们不需要发生的第一个 for 循环之外是可见的(意思是打印值“outside 3”)。原因是如果 var 在函数之外，那么它的**范围就是全局的。但是**让**被**挡住了范围**。这就是为什么当我们试图在循环外访问变量 ***j*** 时，第二个 for 循环会给出错误。**

并且" ***var*** "不会责怪我们，如果我们像下面这样重新声明一个变量。

但是“ ***让”*** 都不会答应去做。

因此，总是喜欢用 ***让*** 或 *const* 而不是 ***var*** 。

# 模板文字

您不再需要使用“+”号连接字符串。有了 ES6，这就容易多了。

字符串应该是**反勾****(`)**，变量应该在 **${}** 内部传递。

如果你使用旧的方法，它看起来会是这样，对于复杂的方法来说，可读性和可管理性较差。

```
const value = "Apple is "+ color;
```

# 多行字符串

一气呵成就能写出多行字符串！

这里我们也需要使用**反勾**。

想象一下我们用老方法做这件事。

看看现代的方法有多简单！。

# 箭头功能

这就是我们通常在 JavaScript 中定义函数的方式。

ES6 提供了一种更加简洁的编写函数的方式。

这个和第一个完全类似。**同样值得记住的是，箭头函数和函数声明并不总是可以互换的。**

# 承诺

当我们需要处理异步任务时，承诺非常有用。

例如，如果我们需要在给定的时间后执行一些，我们可以这样做。它将在两秒钟后打印 console.log()语句。

当您从数据库和 API 获取数据时，这将非常有用。

如果想了解更多关于异步的本质和处理，可以参考这个。

[](https://blog.devgenius.io/handling-asynchronous-nature-in-nodejs-javascript-66471aef6dae) [## 处理 NodeJS/JavaScript 中的异步特性

### 回调，承诺和 Asnyc-await 简单解释

blog.devgenius.io](https://blog.devgenius.io/handling-asynchronous-nature-in-nodejs-javascript-66471aef6dae) 

# 解构

这个特性提供了一种非常简单的方法来解包数组和对象中的值。

我们可以将析构特性应用于一个对象，如下所示。

我们可以对数组做同样的事情。

# for…of 循环

for…of 循环是 ES6 提供的另一个有前途的特性。

代码比使用传统的 for 循环要干净得多。我们可以毫不费力地遍历数组。

# 展开运算符和静止参数

Spread 运算符执行的是对数组中的值进行解包。

作为它的一个用例，这在连接数组时非常有用。

Rest 参数帮助我们通过参数为函数提供任意数量的值。

我已经讨论了 ES6 的几个特性，它们使 JavaScript 变得更加简单。然而，ES6 中有更多的特性，比如类和模块。尽量用 ES6 少写代码多做！。

希望这对你有帮助。编码快乐！

谢谢你。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***