# 如何在 JavaScript 中使用 Array.fill()

> 原文：<https://javascript.plainenglish.io/how-to-use-array-fill-in-javascript-f972d9fce156?source=collection_archive---------11----------------------->

## 探索 JavaScript fill()方法。

![](img/97926dba5c856a420e2234c23f712ca9.png)

Photo by [Kaleidico](https://unsplash.com/@kaleidico?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 最强大的特性之一是它的数组操作能力。只需几行代码，您就可以做出惊人的事情。在这篇博文中，我们将探索这样一种能力:`fill()`方法。这个方法允许你用一个给定的值填充一个数组，使得创建预定值的数组变得非常容易。

## Array.fill()的剖析

`fill()`方法接受三个参数:填充数组的值、起始索引和结束索引。开始和结束索引是可选的；如果忽略它们，填充操作将默认为数组长度的起始索引 0 和结束索引。

## Array.fill()的默认行为

正如我们所讨论的，如果省略可选的开始索引和结束索引参数，`fill()`将用给定值填充从索引 0 到最后一个索引的整个数组。让我们来看看实际情况:

```
const arr = [0, 0, 0];arr.fill(42);console.log(arr); // [42, 42, 42]
```

在上面的代码片段中，我们创建了一个包含三个零的数组。然后我们使用`fill()`用值 42 填充整个数组。当我们将 arr 记录到控制台时，我们可以看到该数组的所有索引都被填充了 42。

![](img/2c563a566c8600b5167da12c12bc7240.png)

Photo by [Adolfo Félix](https://unsplash.com/@adolfofelix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 提供开始索引

现在让我们来看看，如果我们提供了开始索引，但省略了结束索引，会发生什么。

```
const arr = [0, 0, 0];arr.fill(42, 1);console.log(arr); // [0, 42, 42]
```

在上面的代码片段中，我们再次创建了一个包含三个零的数组。这一次，当我们使用`fill()`时，我们提供了一个起始索引 1。这告诉`fill()`从索引 1 开始填充数组。默认行为是结束索引，所以`fill()`用 42 填充从索引 1 到最后一个索引的整个数组。当我们将 arr 记录到控制台时，我们可以看到只有索引 1 和索引 2 填充了 42，而索引 0 保持不变。

## 提供开始和结束索引

现在让我们看看当我们提供开始索引和结束索引时会发生什么。

```
const arr = [0, 0, 0, 0, 0, 0];arr.fill(42, 2, 4);console.log(arr); // [0, 0, 42, 42, 0, 0]
```

在上面的代码片段中，我们创建了一个包含六个零的数组。然后我们使用`fill()`用 42 填充数组，从索引 2 开始，到索引 4 结束。当我们将 arr 记录到控制台时，我们可以看到只有索引二和三被填充了 42；所有其他指数保持不变。如您所见，开始索引是包含性的，而结束索引是排他性的。因此，我们没有用给定的值填充数组中的结束索引。

## 结论

`fill()`方法是一个强大的工具，可以用来在 JavaScript 中轻松操作数组。我希望这篇文章能教会你一些东西。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*