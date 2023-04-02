# 如何计算 JavaScript 数组中元素的和与平均值？

> 原文：<https://javascript.plainenglish.io/how-to-compute-the-sum-and-average-of-the-elements-in-a-javascript-array-e4e8bb5928c?source=collection_archive---------3----------------------->

![](img/324b842ec7309cdd1112973959c7f9dd.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望计算 JavaScript 数组中元素的总和或平均值。

在本文中，我们将研究如何计算 JavaScript 数组中元素的总和及平均值。

# 使用循环

我们可以使用 for-of 循环遍历一个数组，将所有的数字加在一起计算总和。

然后，为了计算平均值，我们可以将总和除以数组的长度。

例如，我们可以写:

```
const arr = [1, 2, 3]
let sum = 0;
for (const a of arr) {
  sum += a;
}const avg = sum / arr.length;
console.log(sum)
console.log(avg)
```

我们定义了一个包含一些数字的`arr`数组。

然后我们定义`sum`变量，并将其初始化为 0。

接下来，我们添加 for-of 循环来遍历`arr`条目。

`a`拥有正在循环的`arr`条目。

在循环体中，我们将`a`值加到`sum`上。

然后我们创建`avg`变量，并将`sum`和`arr.length`的商赋给它。

因此，`sum`为 6，`avg`为 2。

# 使用 Array.prototype.reduce 方法

我们还可以使用 array `reduce`实例方法来计算总和。

然后我们可以用和前面例子一样的方法计算平均值。

例如，我们可以写:

```
const arr = [1, 2, 3]
const sum = arr.reduce((partialSum, a) => partialSum + a, 0)
const avg = sum / arr.length;
console.log(sum)
console.log(avg)
```

`reduce`方法接受具有`partialSum`和`a`的回调。

其中`partialSum`是将被迭代的`arr`条目相加后返回的部分和。

`a`是正在被迭代的`arr`的条目。

回调返回新的部分和。

第二个参数是`sum`的初始值。

代码的其余部分是相同的，我们得到的结果与前面的例子相同。

# 洛达什总和平均法

Lodash 的`sum`方法返回数组条目的总和。

`mean`方法返回数组条目的平均值。

例如，我们可以写:

```
const arr = [1, 2, 3]
const sum = _.sum(arr)
const avg = _.mean(arr)
console.log(sum)
console.log(avg)
```

这两种方法都将我们想要用来进行计算的数组作为参数。

然后我们得到和以前一样的结果。

# 结论

我们可以使用 Lodash 或普通 JavaScript 来计算数组条目的和与平均值。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*