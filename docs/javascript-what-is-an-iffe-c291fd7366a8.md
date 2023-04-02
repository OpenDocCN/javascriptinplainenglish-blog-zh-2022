# JavaScript:什么是 IFFE？

> 原文：<https://javascript.plainenglish.io/javascript-what-is-an-iffe-c291fd7366a8?source=collection_archive---------11----------------------->

![](img/4a27da9cf1e792687362d9cb624fc5cf.png)

Photo by [Mr. Bochelly](https://unsplash.com/@bochelly?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

直接调用函数表达式，简称 IIFEs，是 JavaScript 中的一种常见模式。它们是在同一个语句中定义并立即调用的匿名函数。在本文中，我们将探索 JavaScript 中 IIFEs 的基础知识，包括它们如何工作以及如何在您的代码中使用它们。

## IFFEs 简介

IIFEs 是在同一个语句中定义并立即调用的匿名函数。它们通常用于在脚本或模块中创建局部作用域，这对于组织和整理您的代码非常有用。这里有一个 JavaScript 生活的例子:

```
(function() {
  // Function body
})();
```

在这个例子中，我们有一个在括号中定义的匿名函数。该函数没有名字，由语句末尾的括号立即调用。这会导致函数立即执行，而不需要通过名称调用它。

![](img/bd33a40df245aaa8102a6149520ee960.png)

Photo by [Adolfo Félix](https://unsplash.com/@adolfofelix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 如何使用生命

要在代码中使用 IIFE，只需在括号内定义一个匿名函数，然后通过在语句末尾添加括号来立即调用该函数。下面是一个如何使用 IIFE 在脚本中创建局部作用域的示例:

```
(function() {
  const name = "John";
  console.log(`Hello, ${name}!`);
})();
```

在这个例子中，我们有一个定义了一个`name`变量的生命，然后使用`name`变量打印一个问候。因为`name`变量是在生命中定义的，所以它只能在生命的局部范围内访问。这意味着不能从生命之外访问或修改`name`变量。

IIFEs 对于在脚本或模块中创建局部范围很有用，这有助于防止变量冲突，并提高代码的组织性和可读性。

## 结论

IIFEs 是 JavaScript 编程语言中的一种常见模式。它们是在同一个语句中定义并立即调用的匿名函数，通常用于在脚本或模块中创建局部作用域。希望这篇文章教会你一些东西！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***