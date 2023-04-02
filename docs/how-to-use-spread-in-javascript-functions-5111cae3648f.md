# 如何在 JavaScript 函数中使用 Spread

> 原文：<https://javascript.plainenglish.io/how-to-use-spread-in-javascript-functions-5111cae3648f?source=collection_archive---------4----------------------->

## 了解函数中的 JavaScript spread 运算符

![](img/d864661cb1013413c62daceb2dac4aa7.png)

## 什么是传播？

扩展运算符是由 ES6 引入的，它由三个点(…)组成。根据你在哪里以及如何使用 spread，你可以实现很多事情。spread 的三个主要用途是在函数、对象和数组中。大多数扩展状态的定义都允许你将一个 *iterable* 扩展到另一个地方，比如一个变量。iterable 是一种可以迭代的数据结构。例如，当我们遍历一个数组中的每个元素时，我们就是在迭代这个数组。

## 我们为什么要使用 spread？

JavaScript 有一组附加到内置数学对象的方法，当我们使用这些方法时，这些方法可以让我们从传入的一组值中找到最小和最大值。它们是 Math.max()和 Math.min()。如果我们想从一组数字中找出最小值，我们可以使用 Math.min()方法。让我们来看看这是如何工作的。

```
Math.min(10, 9, 8, 7);//Returns ---> 7
```

在上面的例子中，我们使用了 Math.min()方法，并将其传递给调用四个独立参数的函数，JavaScript 遍历这些值并返回最小值。这很好，但是如果我们的值存储在一个数组中呢？

```
const values = [10, 9, 8, 7];
Math.min(values);//Returns ---> NaN
```

这次我们尝试使用 Math.min()方法，但是我们传入了一个包含值的数组。我们把南带回来。这背后的原因是该函数将接收整个数组作为一个参数。它需要数组中的值作为单独的参数。这是我们可以使用 spread 的地方，因为数组将被分解成单独的元素。让我们尝试同样的例子，但是这次使用 spread 操作符。

```
const values = [10, 9, 8, 7];
Math.min(...values);//Returns ---> 7
```

这次我们返回了 7。如果在函数调用的括号内使用 spread(作为一个参数),那么传递给函数参数的 iterable 将被分割成单独的参数。当我们在上面的例子中使用 spread 时，函数接收四个独立的参数。

## 在函数中使用 spread

我们也可以在函数中使用 spread。如果我们在函数的括号中列出将要使用的参数，并在调用函数时使用 spread 传递一个 iterable，我们就可以访问各个元素。让我们看看这个。

```
function total(first, second, third) {
  return first + second + third
}const vals = [1, 2, 3];
total(...vals);//Returns ---> 6
```

我们创建一个名为 *total* 的函数。在函数的括号内，我们将*第一个*、*第二个、*和*第三个*设为参数。该函数本身返回这些值相加的总和。接下来，我们声明一个名为 *values* 的数组，并为其分配一个包含三个元素的数组。当调用 *total* 函数时，值数组作为参数传递给 *total* 函数。它使用 spread 运算符，因此数组被分割成单独的元素。当功能运行时，第一个*设置为 1，第二个*设置为 2，第三个*设置为 3，因此返回 6。*

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的**[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***