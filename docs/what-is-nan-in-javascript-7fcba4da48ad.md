# JavaScript 中的 NaN 是什么？

> 原文：<https://javascript.plainenglish.io/what-is-nan-in-javascript-7fcba4da48ad?source=collection_archive---------19----------------------->

## 理解 JavaScript 中的 NaN

![](img/0f710a98513d1738e29aa1ce153244dc.png)

## 南是什么？

在 JavaScript 中，NaN 代表一个非数字的值。NaN 实际上是一个数值，但它用来表示任何不能用作数字的东西。由于 NaN 不是一个有效的数字，您不能用它来执行计算。下面是一个例子。

```
5 + NaN;
//Returns ---> NaNNaN * 3;
//Returns ---> NaN0 / NaN;
//Returns ---> NaN
```

如果您尝试执行如下无效计算，也会返回 NaN。

```
0/0;
//Returns NaN
```

在上面的例子中值得注意的是，当你在计算器上执行这个计算时，你会收到一个消息*而不是一个数字*。

## 将 NaN 赋给变量

您可以将 NaN 赋给一个变量，就像您赋给任何其他值一样。为此，您可以将 NaN 直接赋给变量，也可以使用 Number 属性 NaN —这两者是相同的。NaN 本身是全局对象的一个属性，因此可以从任何地方直接使用它。以下是这方面的例子。

```
let one = NaN;
console.log(one);
//Returns ---> NaNlet two = Number.NaN;
console.log(two);
//Returns ---> NaN
```

## NaN 是一个错误

您可能会在代码中遇到 NaN 错误。其中的一些例子包括试图解析一个无效的数字，比如以字母开头的数字。

```
console.log(parseInt('a123'); 
```

另一个例子是试图执行无效的计算，如 undefined。

```
console.log(1 + undefined);//Returns ---> NaN
```

此外，如果您试图将一个无效数字传递给数学运算符，您将得到 NaN。 *sqrt* 方法只接受正数，如下所示。

```
console.log(Math.sqrt(-11));
```

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*