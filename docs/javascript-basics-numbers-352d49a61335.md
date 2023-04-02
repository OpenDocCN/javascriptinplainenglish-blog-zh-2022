# JavaScript 基础:数字

> 原文：<https://javascript.plainenglish.io/javascript-basics-numbers-352d49a61335?source=collection_archive---------9----------------------->

## JavaScript 中的数字

![](img/4e04bdf331098bbc85920a47aaa834a5.png)

Photo by [Mick Haupt](https://unsplash.com/@rocinante_11?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，数字是一种数据类型。它可以保存数字。JavaScript 使用 64 位存储一个数字。可以表示的数的大小是有限的。有了 64 位二进制数字，你可以存储非常大的值。我们说的是万亿分之一的数字。但是一旦你考虑到小数，以及小数点是如何用掉几个位的，那么 64 位中可以容纳的整数的最大数量大约是 9 千万亿。随便啦。不管怎样，它仍然很大。

此外，还有其他数字类型也表示。一个例子是分数，它是这样写的:

```
3.42
```

对于非常大(或非常小)的数字，您可以使用科学记数法，在数字的指数后面加上一个 *e* (代表指数)。它是这样写的:

```
5.435e5
```

上面的数字计算为 5.435 x 10⁵ = 543，500。

还有一些负数也是这样写的:

```
-34
```

请记住，小于千万亿次的数字是精确的。但那是整数。一旦你进入分数，那么精度就不能保证了。即使得到像 pi 这样的数字，JavaScript 也会损失一些精度，因为位数有限。如果您正在处理大的十进制数，JavaScript 对它们的计算更像是近似值，而不是精确值。

## **算术**

通常，当你在 JavaScript 中处理数字时，会涉及到算术。

您可以添加数字:

```
3 + 5
```

减去数字:

```
6 - 2
```

相乘:

```
3 * 6
```

划分:

```
10 / 5
```

数学符号被称为运算符。JavaScript 将输出上述数字的答案。但是你不局限于一次做一个方程，你也可以像这样组合它们:

```
3 + 4 + (4 * 12) / 2
```

你会注意到上面有一个括号。括号有助于对计算进行分组。一旦一个数学方程涉及到括号，你就不能仅仅从`3 + 4`开始，然后继续到`(4 * 12)`，然后除以`2`。您需要先将括号内的数字相乘，然后将该数字除以`2`，再将结果加到`3`和`4`中。为什么？

运算符有一个优先级。把它想象成 PEMDAS。

p-括号

e-指数

m-乘法

d-分部

A —添加

s-减法

你可能也听过这个短语，*请原谅我亲爱的萨莉阿姨，*来帮助你记住这个缩写。

还有一个上面没有提到的运算符，那就是模 or %。这个运算符的作用是输出两个数相除的余数。

```
10 % 5 = 0
```

在上面的例子中，余数将是`0`,因为`10`被等分为`5`。

```
6 % 4 = 2
```

在上面的例子中，`4`只进入 6 一次，剩下`2`作为余数。

## 特殊号码

JavaScript 中有三个特殊的值被认为是数字，但是你不能像普通数字一样使用它们。

前两个是`Infinity`和`-Infinity`，分别代表正负两个无穷大。

另一个是`NaN`，它“不是一个数字”例如，当您试图计算`0 / 0`或`Infinity — Infinity`或任何没有意义的数字计算时，通常会得到这个值。

如果您想阅读更多的 JavaScript 基础知识文章，可以看看这些文章:

[](https://endubueze00.medium.com/javascript-basics-string-concatenation-with-variables-and-interpolation-deba239debbe) [## JavaScript 基础:变量和插值的字符串连接

### 在 JavaScript 中，我们可以将字符串赋给一个变量，并使用串联将该变量组合成另一个字符串。

endubueze00.medium.com](https://endubueze00.medium.com/javascript-basics-string-concatenation-with-variables-and-interpolation-deba239debbe) [](/javascript-basics-variables-cb58d26167f9) [## JavaScript 基础:变量

### 在 JavaScript 中，您可以使用变量来标记任何类型的数据。变量就像盒子，里面贴着标签，告诉你…

javascript.plainenglish.io](/javascript-basics-variables-cb58d26167f9) [](https://levelup.gitconnected.com/javascript-basics-mathematical-assignment-operators-e888e78fd391) [## JavaScript 基础:数学赋值运算符

### 在 JavaScript 中做数学运算时，您可能希望继续增加值。我们可以通过以下组合来实现这一点…

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-basics-mathematical-assignment-operators-e888e78fd391) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***