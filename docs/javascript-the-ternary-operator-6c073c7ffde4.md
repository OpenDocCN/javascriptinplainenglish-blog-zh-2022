# JavaScript:三元运算符

> 原文：<https://javascript.plainenglish.io/javascript-the-ternary-operator-6c073c7ffde4?source=collection_archive---------13----------------------->

![](img/558273a4a553177fe407ef5c37497f0e.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nublson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

三元运算符是一个简单但功能强大的工具，可以在 JavaScript 代码中使用。它允许您评估一个条件，如果条件为真，则返回一个值，如果条件为假，则返回另一个值。在这篇博文中，我们将探讨三元运算符是如何工作的，以及如何在自己的代码中使用它。

## 三元算子的结构

三元运算符由三部分组成:条件、条件为真时的值和条件为假时的值。这三部分用一个问号(？)和冒号(:)。下面是该运算符的基本结构:

```
condition ? value if true : value if false;
```

让我们来分解这个结构的每个部分。

## 条件

运算符的第一部分是要计算的条件。这可以是任何计算结果为布尔值(真或假)的表达式。例如，您可以使用比较运算符:

```
var x = 100;var y = 50;x > y ? “x is greater than y” : “x is less than or equal to y”; // “x is greater than y”
```

在此示例中，当 x 大于 y 时，条件将评估为真。

## 值是否为真

运算符的第二部分是条件评估为 true 时将返回的值。这可以是任何有效的 JavaScript 表达式。例如，您可以返回一个字符串:

```
var x = 100;var y = 50;x > y ? “x is greater than y” : “x is less than or equal to y”; // “x is greater than y”
```

## 值为假

运算符的第三个也是最后一个部分是条件评估为 false 时将返回的值。同样，这可以是任何有效的 JavaScript 表达式。重复使用前面的例子，如果条件为假，我们可以返回一个字符串，表明 x 小于或等于 y。

```
var x = 30;var y = 50;x > y ? “x is greater than y” : “x is less than or equal to y”; //“x is less than or equal to y”
```

## 三元运算符为什么有用

当您需要根据条件返回一个值，但不想使用 if/else 语句时，三元运算符最有用。例如，考虑以下返回消息“欢迎回来！”的代码如果用户已登录，如果用户未登录，则显示“请登录”:

```
if (user.isLoggedIn) { message = “Welcome back!”;} else { message = “Please log in”;}
```

这段代码运行良好，但是可以使用三元运算符写得更简洁:

```
message = user.isLoggedIn ? “Welcome back!” : “Please log in”;
```

正如您所看到的，三元运算符提供了一种更简洁的方式来编写这种类型的代码。

## 结论

三元运算符是一个简单但功能强大的工具，可以在 JavaScript 代码中使用。它允许您评估一个条件，如果条件为真，则返回一个值，如果条件为假，则返回另一个值。我希望这篇文章教会了你如何使用三元运算符的基础知识。祝你的编码项目好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*