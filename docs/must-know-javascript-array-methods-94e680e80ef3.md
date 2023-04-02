# 必须知道的 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/must-know-javascript-array-methods-94e680e80ef3?source=collection_archive---------12----------------------->

![](img/c93a948635aed762a26cccd9bbe0f8d6.png)

Photo by [Kaleidico](https://unsplash.com/@kaleidico?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你是一名 JavaScript 开发人员，了解这门语言的来龙去脉是很重要的。一个特别重要的主题是数组。数组是 JavaScript 中最基本的数据结构之一，几乎在每个项目中都要用到。在这篇博文中，我们将讨论一些每个 JS 开发者都应该知道的最基本的数组方法。

## forEach()

我们将讨论的第一个方法是`forEach()`方法。此方法允许您迭代数组并对每个元素执行特定的操作。例如，假设您有一个数字数组，您想将它们打印到控制台上。您可以这样做:

```
let nums = [1, 2, 3]nums.forEach(num => console.log(num)); //prints out 1 2 3
```

`forEach()` 方法非常适合简单的迭代，但是它不能给你很多控制。如果您需要尽早退出循环或访问当前元素的索引，您需要使用不同的方法。

## 地图()

`map()`方法与`forEach()`非常相似，但是它返回一个包含回调函数结果的新数组。例如，假设您有一个数字数组，您想对每个数字求平方。您可以这样做:

```
let nums = [0, 2, -100];let squaredNums = nums.map(num => num * num);return squaredNums //returns [0, 4, 10000]
```

## 减少()

`reduce()` 方法允许你将一个数组缩减为一个值。这是通过使用回调函数将数组中的元素组合在一起实现的。例如，假设你有一个数组，你想把它们加在一起。您可以这样做:

```
let nums = [0, -100, 33];let sum = nums.reduce((accumulator, currentValue) => {return accumulator + currentValue;}, 0);console.log(sum); //returns -67
```

`reduce()`方法有两个参数:回调函数和累加器的初始值。回调函数本身有两个参数:累加器和当前值。在这个例子中，我们从 0 开始累加器，并把数组中的每个元素都加进去。

## 过滤器()

`filter()`方法允许你创建一个新的数组，只包含通过特定测试的元素。例如，假设你有一个数字数组，你只想得到正数。您可以这样做:

```
let nums = [-100, 0, 33];let positiveNums = nums.filter(num => num > 0);console.log(positiveNums); //returns [33]
```

`filter()`方法将回调函数作为参数。这个回调函数必须返回一个布尔值(真或假)。返回 true 的元素被添加到新数组中，而返回 false 的元素被忽略。

## 切片()

`slice()` 方法允许您从现有数组的一部分创建一个新数组。例如，假设您有一个数字数组，您想要前三个元素。您可以这样做:

```
let nums = [0, -100, 33, 12, -200];let firstThree = nums.slice(0, 3);console.log(firstThree); //returns [0, -100, 33]
```

`slice()`方法有两个参数:开始索引和结束索引。包含起始索引处的元素，但不包含结束索引处的元素。

## 拼接()

方法允许你从数组中移除元素。例如，假设您有一个数字数组，您想删除前两个元素。您可以这样做:

```
let nums = [0, -100, 33, 12, -200];nums.splice(0, 2);console.log(nums); //returns [33, 12, -200]
```

`splice()`方法有两个参数:起始索引和要移除的元素数量。

## 包括()

`includes()`方法允许你检查一个数组是否包含某个元素。例如，假设您有一个数字数组，您想知道它是否包含数字 33。您可以这样做:

```
let nums = [0, -100, 33, 12, -200];console.log(nums.includes(33)); //returns true
```

`includes()`方法有一个参数:要搜索的元素。如果找到该元素，则返回 true。否则，它返回 false。

## 排序()

`sort()`方法允许你对数组中的元素进行排序。`Array.sort()`接受可选参数 compareFunction。如果未提供此参数，数组将默认为按字典升序排序(字典顺序)。`sort()` 方法经常让开发人员感到困惑，需要更多的解释和练习。请随意查看我在`Array.sort()`上写的这篇[文章](https://medium.com/@alexzelinsky124/how-to-use-javascripts-array-sort-53651730c580)，其中我用多个例子解释了这个方法。

这就是必须知道的数组方法！请务必练习它们，这样您就可以在代码中流畅地使用它们。祝你的编码面试好运！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***