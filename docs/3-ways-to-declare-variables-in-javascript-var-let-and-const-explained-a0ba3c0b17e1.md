# 解释了在 JavaScript 中声明变量的 3 种方法:var、let 和 const

> 原文：<https://javascript.plainenglish.io/3-ways-to-declare-variables-in-javascript-var-let-and-const-explained-a0ba3c0b17e1?source=collection_archive---------18----------------------->

![](img/671c88b05d3e2e284e1fe1176ada5f3a.png)

在写这篇文章的时候，JavaScript 中只有*两种*流行的声明变量的方式:`let`和`const`；可怜的 T2 长期迷失在被误解的原则的黑暗中。

写这篇文章背后的想法是试图澄清为什么新开发人员对使用`var`持怀疑态度，每次我在采访中问这个问题，我听到的都是“var 不好”、“var 产生全局变量”，等等等等。

# TL；博士；医生

*   `var`函数是有作用域的吗？也就是说，它只能在声明它的函数的作用域内被访问。
*   `let`和`const`是块范围的，也就是说，它们只能在声明它们的块范围内被访问。

那些正在寻找更深入解释的人应该继续阅读。

![](img/1ecc88f9dea207fed6057f6812168e43.png)

# 定义变量

`var`有史以来就有了(开个玩笑，我觉得甚至在那之前就有了)。使用`var`声明的变量的一些特征:

*   当在函数内部定义时，它是函数范围的，否则是全局范围的。
*   可以在相同的范围内重新声明它，而不会抛出错误(即使在严格模式下)。
*   它可以被重新分配。
*   可以用在代码中的声明行之前(虽然值会是`undefined`)。

```
console.log(test); // undefined

var test = "512";

console.log(test); // 512
```

因为解释器会看到这样的代码:

```
var test; // undefined is the default value
console.log(test); // undefined
test = "512"
console.log(test); // 512
```

# const and let

除了使用`const`声明的变量不能被重新赋值之外，`const`和`let`的行为是相同的。

使用`const`和`let`声明的变量的一些特征:

*   当在一个内部定义时，它们是块范围的，否则是全局范围的。
*   它们不能重新声明。
*   使用`let`声明的变量可以重新赋值，但`const`不能。
*   它们不能用在代码中的声明行之前(因为变量不是给定的默认值，所以会引发引用错误)。

```
console.log(test); // ReferenceError: Cannot access 'test' before initialization

var test = "512";

console.log(test);
```

# 结论

每种工具都是为某种目的而制造的，我们应该利用它的优点，而不是一味地批评它。

我将写另一篇文章解释我们如何最好地使用这些工具。

这一次到此为止。希望这篇文章对你有帮助！如果您有任何反馈或问题，请随时在下面的评论中提出。更多此类文章，请在 [Twitter](https://twitter.com/sun_anshuman) 关注我。

下次见！

![](img/dd5fc2e459d45c5fd5faa5565ae90f7f.png)

*原载于 2022 年 4 月 11 日*[*https://theanshuman . de*v](https://theanshuman.dev/articles/3-ways-to-declare-variables-in-javascript-var-let-and-const-explained-45am)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***