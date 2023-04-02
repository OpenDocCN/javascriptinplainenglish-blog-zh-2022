# 双爆炸(！！)和 JavaScript 类型强制

> 原文：<https://javascript.plainenglish.io/double-bang-and-javascript-type-coercion-a554a44c5652?source=collection_archive---------5----------------------->

## 深潜双爆炸(！！)和 JavaScript 中的类型强制。

![](img/b6d474f5a321ca97d1fc062a7117d371.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

第一次看到两个 bang 算符写在一起，觉得很荒谬，多余。研究表明，在很大程度上，我是对的。双爆炸看起来几乎像是过去的开发人员留下的古老符号，用来表示变量何时应该是布尔值。让我们深入探讨一下。

在继续之前，我们应该消除一些人可能有的误解:double bang，written `!!`不是运算符。它只是两个单个的`!` bang 运算符依次使用。此外，我们应该理解类型*强制*和类型*转换之间的区别。*

## 类型强制

类型强制是类型转换的子集。转换是一种数据类型与另一种数据类型之间的转换，例如将数字转换为字符串，将字符串转换为浮点数等。有两种类型的转换—显式和隐式。当使用函数将变量从一种数据类型显式转换为另一种数据类型时，会发生显式类型转换。一个例子是

```
var pointNum = Number(text);
```

其中`text`是一个被转换成数字的字符串。

隐式类型转换也称为类型强制。当变量被视为另一种数据类型时，即使没有发生转换过程，也会出现这种情况。一个例子是

```
const stringNum = '6';
const realNum = 7;
var sum = value1 + value2; // Sum is '67'
```

其中数字`7`被添加到字符串`'6'`中。由于数字不能以有意义的方式添加到字符串中，JavaScript 将数字转换为字符串并追加，使`sum`等于`'67'`而不是 13。如果您没有意识到它的含义，类型强制可能会导致问题，但它也可以是简化代码的工具。

## 双爆炸

这就是“双重爆炸”的由来。考虑以下代码:

```
const name = '';
var bangName = !name;
```

你知道`bangName`会评价到什么吗？在我们回答这个问题之前，让我们再绕一小段路来讨论真假价值观。

如果在强制进入布尔上下文时，一个值的计算结果为 true，则该值被视为“真”。同样，如果计算结果为 false，则为“falsy”。虚假值的一些例子是:

```
false (boolean)
0 (number)
'' (empty string)
null
undefined
```

因此，像`if ('')`这样的东西不会执行它的内部代码，因为它的计算结果不是 true。

在上面的例子中，`bangName`将等于`true`，因为空字符串是 falsy，而我们的 bang 操作取相反的结果，即`true`。现在让我们加上第二次爆炸:

```
const name = '';
var doubleBangName = !!name;
```

显然，由于单次爆炸的计算结果为`true`，添加第二次爆炸将使其计算结果为`false`。那么这有什么用呢？

实际上，通常不会。双爆炸带来的价值是清晰的，即使如此也很少。很少有这样的情况，它在功能上给代码增加了一些东西。然而，双击可以用来向其他开发人员或您未来的自己表明，一个语句的计算结果应该是布尔值。当需要将变量转换为布尔值时，也可以使用它，例如在函数返回中:

```
return items.length > 0;
```

可以简化为:

```
return !!items;
```

刚发现的时候，开始频繁使用双刘海。后来，我了解了更多关于真假价值观的知识，意识到自己一事无成。这取决于你是否相信使用它会提高代码的清晰性或完成任何有用的事情。和所有事情一样，它只是你工具箱中的另一个工具。

感谢阅读。欲了解更多信息:

[](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) [## Truthy - MDN 网络文档词汇表:网络相关术语的定义| MDN

### 在 JavaScript 中，真值是在布尔上下文中遇到时被认为是真的值。所有值都是…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) [](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) [## Falsy - MDN 网络文档词汇表:网络相关术语的定义

### falsy(有时写为 false)值是在布尔上下文中遇到时被视为 false 的值。

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) [](https://developer.mozilla.org/en-US/docs/Glossary/Type_Conversion) [## 类型转换- MDN Web 文档词汇表:Web 相关术语的定义| MDN

### 类型转换(或类型转换)意味着将数据从一种数据类型转换为另一种数据类型。隐式转换发生在…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/Type_Conversion) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***