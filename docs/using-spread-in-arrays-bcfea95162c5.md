# 如何在 JavaScript 数组中使用 Spread

> 原文：<https://javascript.plainenglish.io/using-spread-in-arrays-bcfea95162c5?source=collection_archive---------5----------------------->

## 如何在数组中使用扩展运算符的指南

![](img/7e620a1c1f0fe45823bb3b6a1cfc4488.png)

我最近发表了一篇[文章](https://medium.com/@codecupdev/how-to-use-spread-in-javascript-functions-5111cae3648f)介绍了 spread 操作符以及如何在函数中使用它。本文的后续部分将会介绍如何对数组使用 spread 操作符。

当你使用数组时，如果你想复制一个数组或者合并多个数组，那么 spread 操作符非常有用。当你在一个数组中使用 spread 操作符时，它会将内容扩散到另一个数组中。原始数组将保持不变。让我们看一个基本的例子。

```
const first = [1, 2, 3];
const second = [4, 5, 6];
const countToSix = [...first, ...second];console.log(countToSix);
//Returns ---> //(6) [1, 2, 3, 4, 5, 6]
```

在上面的例子中，我们声明了一个名为 *first* 的变量，并给它分配了一个包含三个值的数组；我们声明了另一个名为 *second* 的变量，也给它分配了一个包含两个值的数组。接下来，我们声明另一个名为 *countToSix* 的变量。我们给 *countToSix* 分配一个数组，该数组使用 spread 操作符传入第一个*数组*和第二个*数组*。当我们控制台记录 *countToSix* 变量时，我们得到一个包含第一个*和第二个*数组的所有元素的数组。

当对数组使用 spread 运算符时，值得注意的是，顺序确实很重要，这取决于您希望数组中的元素如何排序。我们还可以在使用 spread 运算符的元素旁边添加其他元素，如下例所示。

```
const first = [1, 2, 3];
const second = [4, 5, 6];
const countToSeven = [...first, ...second, 7];console.log(countToSeven)
//(7) [1, 2, 3, 4, 5, 6, 7]
```

如果您使用 spread 来复制数组，那么它们将不会彼此相等，因为数组是通过引用而不是通过值来存储的，所以它是对存储在计算机内存中的数组的引用，而不是数组本身的值，但这不适用于嵌套数据结构。

```
const initialArray = ["a", "b", "c"];
const copyInitialArray = [...initialArray];initialArray === copyInitialArray//Returns ---> false
```

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*