# 大多数开发人员不知道的 6 个很酷的现代 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/6-cool-modern-javascript-features-most-developers-dont-know-about-432f7652dd4c?source=collection_archive---------0----------------------->

## 编写简明 JavaScript 代码的技巧

![](img/6f7f9959b65f75351a04409baf535b29.png)

# 前言

JavaScript 在不断进化升级，越来越多的新特性让我们的代码变得简洁。本文将介绍六个新的 JavaScript 特性。让我们一起来研究它们。

# 1.使用“Object.hasOwn”而不是“in”运算符

有时，我们想知道一个属性是否存在于一个对象上，并使用“in”操作符或“obj.hasOwnProperty”来这样做。但两者都有一些瑕疵，我们来看看。

**“in”运算符**

如果指定的属性在`specified object` 或其`prototype chain`中，则“in”运算符返回`true`。

**obj.hasOwnProperty**

`hasOwnProperty`方法返回一个布尔值，表明对象是否有指定的属性作为它的`own property`(与继承它相反)。

**使用上面相同的例子:**

也许`"obj.hasOwnProperty"`已经可以过滤掉原型链上的属性了，但是在某些情况下并不安全，会导致程序失败。

**Object.hasOwn**

不用担心，我们可以用“Object.hasOwn”来避免这两个问题，比“obj.hasOwnProperty”方法更方便，也更安全。

# 2.使用“#”声明私有属性

过去，我们使用`"_"`来表示私有属性，但是它并不安全，仍然可能被外部修改。

**我们可以使用“#”来实现真正安全的私有属性:**

# 3.有用的数字分隔符

我们可以用“_”让数字更易读。很酷。

当然，我们可以使用“_”进行实际计算。

# 4.用“？."简化“&&”和三元运算符

下面的例子你一定很熟悉，我们可以简化一下吗？

用“？."简化您的代码。

**提示**

“的常见拼法？."

1.  `obj?.prop`对象属性
2.  `obj?.[expr]`对象属性
3.  `func?.(...args)`函数或对象方法的调用

# 5.用“？?"而不是“||”

用“？?"代替“||”，用来判断运算符左边的值是`null`还是`undefined`，然后返回右边的值。

# 6.使用“BigInt”支持大整数计算问题

JS 中超过`"Number.MAX_SAFE_INTEGER"`的数字计算不保证正确。

**例如:**

对于大数的计算，可以使用“BigInt”来避免计算错误。

# 最后

**感谢阅读，**在下一篇文章中，我会写关于 **Chrome 的调试技巧。**期待期待您的关注和阅读更多高质量的文章。

[](/interviewer-you-have-been-working-for-3-years-and-you-cant-answer-this-algorithm-question-5f79cba18e06) [## 面试官:你工作 3 年了，这种算法题你都不会答？

### 一个女生的面试经历

javascript.plainenglish.io](/interviewer-you-have-been-working-for-3-years-and-you-cant-answer-this-algorithm-question-5f79cba18e06) [](/8-javascript-tricks-to-make-you-a-better-programmer-948b5a3c35b4) [## 让你成为更好的程序员的 8 个 JavaScript 技巧

### 使用这些代码提示，让您的 JavaScript 更具可读性和可扩展性。

javascript.plainenglish.io](/8-javascript-tricks-to-make-you-a-better-programmer-948b5a3c35b4) [](/my-boss-you-know-es6-but-why-dont-you-use-it-5e0316f14c67) [## 我老板:你知道 ES6，为什么不用？😠

### 老板的 10 条抱怨让我受益匪浅。

javascript.plainenglish.io](/my-boss-you-know-es6-but-why-dont-you-use-it-5e0316f14c67) [](/15-killer-websites-for-web-developers-35a4c007942a) [## 面向网络开发人员的 15 个黑仔网站

### 99.9%的开发者都不知道。

javascript.plainenglish.io](/15-killer-websites-for-web-developers-35a4c007942a) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*