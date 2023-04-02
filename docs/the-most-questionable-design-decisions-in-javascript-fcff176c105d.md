# JavaScript 中最可疑的设计决策

> 原文：<https://javascript.plainenglish.io/the-most-questionable-design-decisions-in-javascript-fcff176c105d?source=collection_archive---------12----------------------->

![](img/6e0782a48a02b64d685123fe4380c0b0.png)

Photo by [Siora Photography](https://unsplash.com/@siora18?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 自 1995 年诞生以来已经走过了漫长的道路。它已经发展成为世界上最流行的编程语言之一。然而，像任何其他语言一样，JavaScript 也有其可疑的设计决策。在本文中，我们将看看 JavaScript 设计者做出的一些最有争议的选择。请记住，并不是每个人都同意这些选择，但它们仍然值得讨论！

## 圆盘烤饼

JavaScript 最有争议的方面之一是它对 NaN(非数字)的处理。当无法执行数学运算时，如 0/0 或`Math.sqrt(-100)`，JavaScript 将返回值 NaN。然而，NaN 的设计是这样的，它不等于任何其他的价值——包括它本身！这可能会导致一些令人困惑的情况，如以下代码所示:

```
console.log(NaN === NaN); // false
```

这意味着您不能使用通常的等式运算符来测试 NaN。相反，您必须使用内置的 isNaN()函数:

```
console.log(isNaN(NaN)); // true
```

NaN 的类型也令人困惑——它实际上是一个数字！

```
console.log(typeof NaN); // “number”
```

这意味着当您对包含 NaN 的变量使用 `typeof`时，它将返回“number ”,即使该值本身不是一个数字。这种功能给开发人员带来了很多困惑，并导致代码难以调试。

## eval()

`eval()`函数是 JavaScript 的另一个有争议的特性。`eval()`获取一串代码并执行，就像它是实际的 JavaScript 代码一样。这在某些情况下可能很有用，但也可能很危险。`eval()`是一种安全风险，因为它允许恶意代码在用户的机器上执行。

调试使用`eval()`的代码也很困难，因为被评估的代码串不是立即可见的。出于这些原因，通常认为最好避免使用`eval()`，除非绝对必要。

## 带有关键字的

`with` 关键字是 JavaScript 的另一个有争议的特性。`with` 允许您为给定的代码块创建一个新的作用域。这在某些情况下可能有用，但也可能导致难以理解的代码。`with` 关键字应该谨慎使用，因为它会使代码变得更加脆弱和难以维护。

![](img/6e131a661f0b695dcde664c6aeff7455.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 原型

JavaScript 的另一个有争议的方面是它对原型的使用。基于原型的编程是面向对象编程的一种风格，其中对象从原型继承它们的属性和行为。这与更常见的基于类的方法不同，在基于类的方法中，对象从类继承。基于原型的编程可能更灵活，但对于习惯于基于类的语言的开发人员来说，它也可能会令人困惑，并导致语法不一致。

基于原型编程的主要优点是使用原型可以更快地创建具有相同属性和行为的对象。使用原型，一个对象的属性和方法可以直接从另一个对象继承，不需要重新创建。

JavaScript 包含了一个类语法，它仅仅是原型之上的语法糖。这使得 JavaScript 对于来自其他语言的开发人员来说变得更加用户友好。

## 结论

二十多年来，JavaScript 一直是最有影响力和最受欢迎的编程语言之一。在此期间，它做出了一些伟大的设计决策——也有一些有问题的决策。这种语言在继续发展和改进，JavaScript 的未来看起来很光明。然而，了解这种语言有争议的方面是很重要的，这样你就可以对何时以及如何使用它们做出明智的决定。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***