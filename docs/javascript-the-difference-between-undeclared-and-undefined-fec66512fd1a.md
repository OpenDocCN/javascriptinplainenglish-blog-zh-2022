# JavaScript:未声明和未定义的区别

> 原文：<https://javascript.plainenglish.io/javascript-the-difference-between-undeclared-and-undefined-fec66512fd1a?source=collection_archive---------2----------------------->

![](img/4083fe1b664d4d39b11408774c0e45c3.png)

Photo by [Boitumelo Phetla](https://unsplash.com/@writecodenow?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

术语“未声明的”和“未定义的”经常在 JavaScript 的世界中引起混乱，但是它们指的是两种非常不同的东西。在这篇博文中，我们将看看这两个术语之间的主要区别，以及它们如何影响您的代码。

## 什么是“未申报”？

当一个变量“未声明”时，意味着它没有在当前范围内声明或定义。换句话说，它还没有被赋予一个值或类型。如果您试图使用一个变量而没有先声明它，或者如果您拼错了变量名，就会发生这种情况。

例如，考虑以下代码:

```
// This code will throw a ReferenceError because the variable "x" is undeclared
console.log(x);
```

这里，`console.log()`语句试图记录`x`变量的值，但是`x`还没有在代码中声明。结果，JavaScript 会抛出一个`ReferenceError`，表示没有定义`x`。

需要注意的是，未声明的变量不同于未初始化的变量。未初始化的变量是那些已经声明但还没有赋值的变量。例如:

```
/* This code will not throw an error because the variable "x" is declared, 
even though it has not been initialized with a value */
let x;
console.log(x); // Output: undefined
```

在这段代码中，`let x`语句声明了`x`变量，但没有用值初始化它。因此，当我们试图记录`x`的值时，输出是`undefined`。

![](img/ce7314950018b441d187d5fad1917137.png)

Photo by [Bench Accounting](https://unsplash.com/@benchaccounting?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 什么是“未定义”？

与“未声明的”变量不同，“未定义的”变量已在当前作用域中声明，但尚未赋值。换句话说，它们已经被初始化，但是它们的值没有被定义。

例如:

```
/* This code will not throw an error because the variable "x" is declared 
and initialized, but its value is undefined */
let x;
console.log(x); // Output: undefined
```

这里，`let x`语句声明了`x`变量并初始化它，但没有给它赋值。因此，当我们试图记录`x`的值时，输出是`undefined`。

理解未声明和未定义变量之间的区别是很重要的，因为它们会在代码中导致不同类型的错误。未声明的变量将抛出一个`ReferenceError`，而未定义的变量不会导致任何错误，但可能会在您的代码中产生意想不到的结果。

## 结论

未声明的变量是那些没有在当前作用域中声明或定义的变量，而未定义的变量是那些已经声明但没有赋值的变量。理解这两个术语之间的区别对于编写正确有效的 JavaScript 代码至关重要。希望这篇文章教会你一些东西！

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*