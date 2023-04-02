# JavaScript:作为一级对象运行

> 原文：<https://javascript.plainenglish.io/javascript-functions-as-first-class-objects-d49b25fe88b3?source=collection_archive---------7----------------------->

## 探索将函数作为一级对象意味着什么，以及随之而来的一些好处。

![](img/dd4a1bb7b789464e0ee47136e3bcceca.png)

Photo by [Seven Shooter](https://unsplash.com/@sevenshooterimage?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当开发者说函数是 JavaScript 中的一级对象时，那是什么意思？在本文中，我们将探讨将函数作为一级对象意味着什么，以及随之而来的一些好处。我们还将看一些例子，说明如何在自己的代码中使用函数作为一级对象。

## 什么是一等物体？

在计算机科学中，一级对象是一种实体，可以在编程语言中以与其他对象相同的方式创建和操作。一级对象支持三种主要操作。

1.  一级对象可以赋给变量
2.  一级对象可以是参数
3.  一级对象可以是返回值

在 JavaScript 中，函数是一级对象。这意味着它们可以像 JavaScript 中的任何其他对象一样被创建和操作。让我们看一些例子来说明这是如何工作的。

## 函数作为变量

首先，让我们看看如何给变量分配函数。在下面的例子中，我们将创建一个函数，它接受两个参数并返回这些参数的和，然后将它赋给一个变量。

```
let adder = function (a, b) { return a + b;}
```

在本例中，我们将加法器函数赋给了一个变量。然后，我们可以使用该变量调用函数，如下所示:

```
let result = adder(20, 30);console.log(result); // prints 50
```

如你所见，我们能够像对待其他变量一样对待函数。我们可以把它赋给一个新变量，然后像调用其他函数一样调用它。

![](img/c2ece5ead1d7d76cf5b0d714ed655cd5.png)

Photo by [Adolfo Félix](https://unsplash.com/@adolfofelix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 作为参数的函数

除了能够将函数赋给变量，我们还可以将它们作为参数传递给其他函数。在下面的示例中，我们将创建一个函数，它将另一个函数作为参数，并使用一对参数调用该函数。

```
let callFunction = function (fn, arg1, arg2) { return fn(arg1, arg2);}
```

在这个例子中，我们创建了一个函数，它将另一个函数作为它的第一个参数。然后，我们可以用提供的两个参数调用前面的加法器函数。

```
let result = callFunction(adder, 20, 10);console.log(result); // prints 30
```

在本例中，我们将加法器函数作为参数传递给了 callFunction 函数。然后，我们能够从 callFunction 函数中调用 adder 函数。

## 用作返回值

最后，我们来看看如何从其他函数返回函数。在下面的示例中，我们将创建一个函数，该函数接受一个参数并返回一个新函数，该函数将所提供参数的值加倍。

```
let doubleValue = function (value) { return function () { return 2 * value; }}
```

在这个例子中，我们创建了一个返回另一个函数的函数。然后，我们可以使用这个函数来乘以我们提供的任何数字的值。

```
let multiplier = doubleValue(20);console.log(multiplier()); // prints 40
```

在本例中，我们调用了参数为 20 的 doubleValue 函数。这返回了一个新函数，它将 20 的值加倍。然后，我们将这个新函数赋给一个变量，并调用它来获得结果。

## 结论

在本文中，我们探讨了在 JavaScript 中将函数作为一级对象意味着什么。我们已经看到了如何将它们赋给变量，将它们作为参数传递给其他函数，并从其他函数返回它们。我们还看到了如何使用这些特性来编写更具表现力和灵活性的代码。

我希望你从这篇文章中学到了一些东西。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***