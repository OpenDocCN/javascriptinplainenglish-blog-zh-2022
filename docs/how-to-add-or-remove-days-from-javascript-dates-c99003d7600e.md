# 如何在 JavaScript 日期中添加或删除日期

> 原文：<https://javascript.plainenglish.io/how-to-add-or-remove-days-from-javascript-dates-c99003d7600e?source=collection_archive---------14----------------------->

## Java Script 语言

在普通 JavaScript 中添加或删除日期类型。

![](img/10bd0905e3b30f1a6a385a5453d45e1e.png)

Photo by [Brooke Campbell](https://unsplash.com/@bcampbell?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当您在处理一个需要时间的项目时，JavaScript 日期操作非常重要。简单的`.add()`和`.subtract()`日期操作没有直接在 JavaScript 中实现，但是我们可以通过自己的实现来实现。

## 1.正在初始化

当我们处于日期创建的前期状态，并且我们可以访问各种类型的日期参数时——我们可以修改传递的输入，日期会相应地改变。

日期修改的一个例子—我们想给`June 15, 2022`增加 5 天。我们只需将数字`5`添加到`days`参数中，该变化将影响日期，即使该数字超过一个月的边缘:

```
new **Date**(2022, 5, 15 + **5**);
```

## 2.设置参数

另一种方法是用相应的值设置参数。我们可以用一个`get`方法来加/减任意数量的日期类型，并将新值设置为该日期的日期类型。

这可能更有用，因为我们在开始时不需要初始化的值，我们可以在以后修改它。

一个设置的例子—我们想从`June 15, 2022`中减去 4 个月。我们按照以下方式设置参数:

```
var **date** = new **Date**(2022, 5, 15);
date.**setMonths**(date.**getMonths()** - 4);
```

## 3.毫秒

另一种方法是通过毫秒设置日期，这可能是最不喜欢的，因为你必须计算一个新的日期，但它仍然可以工作。我们可以添加以毫秒为单位的日期类型的数量，这涉及到很多大整数。

一个以毫秒为单位设置日期的例子——我们想给`June 15, 2022`加上 20 天。我们通过以下方式设置以毫秒为单位的日期:

```
var **date** = new **Date**(2022, 5, 15);
date = new **Date**(date.**getTime()** - 20 * (60 * 1000 * 60 * 24));
```

## 结论

我们可以用很多方法操纵 JavaScript 日期，这些是最流行的方法。看到这些像`.add()`和`.subtract()`这样的基本方法没有直接在 JavaScript 中实现是令人难过的。我希望这篇文章能帮助你理清关于日期的事情。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*