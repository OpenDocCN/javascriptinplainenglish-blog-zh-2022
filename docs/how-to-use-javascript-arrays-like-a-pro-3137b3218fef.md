# 如何像专业人士一样使用 JavaScript 数组

> 原文：<https://javascript.plainenglish.io/how-to-use-javascript-arrays-like-a-pro-3137b3218fef?source=collection_archive---------2----------------------->

![](img/5841d4adbccbb78695847576eb39ad70.png)

Photo by [Glenn Carstens-Peters](https://unsplash.com/@glenncarstenspeters?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/professional--employee?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

> 在本文中，我们将看到使用数组和用数组进行操作的现代方法。这些方法要方便得多，可以帮助你用更少的代码行编写代码。

下面我们就用例子来探讨一下做这些的方法。

## 1.数组.映射()方法

我们可以使用 map()将数组的值转换成另一种形式。假设我们有一个对象数组，这样带有关键字 name 和 age 的对象。

```
const data = [{ name:'Anne', age: 20 }, 
              { name:'Mike', age: 24 }, 
              { name:'Max', age: 27 }, 
              { name:'Sara', age: 25 }, 
              { name:'George', age: 24 }]
```

我们需要得到对象数组的名字，如下所示。

```
[“Anne”, “Mike”, “Max”, “Sara”, “George”]
```

我们可以用 map()做到这一点。

## 2.数组.过滤器()方法

filter()方法的用例是根据给定的条件过滤数组中的元素。假设现在我们需要找到 24 岁以上的人。我们可以使用 filter()方法来做到这一点。

那么输出将如下所示。

```
[{ age: 27, name: “Max” }, { age: 25, name: “Sara” }]
```

所以我们有超过 24 岁的人。

## 3.Array.reduce()方法

reduce 方法可用于根据数组中对象的属性获取单个值。

试想我们需要知道以上人群的平均年龄。我们如何做到这一点？

零是初始值。年龄将被逐一累加并存储在累加器中。最后，它作为函数值返回。除以数组的长度将得到平均年龄。

所以这里的输出是 24。

这些 map()、filter()和 reduce()方法被称为高阶函数。

## 4.传播算子

spread 运算符将对数组的元素进行解包。

假设我们有以下数组。

```
const colors1 = ["red", "green", "blue"]
const colors2 = ["yellow", "white", "black"]
```

如果我们需要连接这两个数组，我们可以使用 spread 操作符。就一句台词。

spread 运算符的另一个用例是克隆一个数组。假设我们需要克隆下面的数组。

```
const colors = ["red", "green", "blue"]
```

我们可以这样做。

请注意检查两个数组相等的最后一行代码。这是假的。这是因为它创建了给定数组的浅表副本。

## 5.数组析构

假设我们有一个如下的数组。

```
const colors = ["red", "green", "blue"]
```

如果我们需要得到数组的值，传统的方法是什么？

但是我们可以使用 ES6 的析构特性以更好的方式做到这一点。

输出将是，

```
“red”, “green”, “blue”
```

想象一下使用传统的方法如 for-loops 来做上述事情。将会有许多代码，但是使用这些现代的方法将会使我们的生活更容易。代码将易于修改、调试、阅读和处理。

希望这对你有帮助。

谢谢大家！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*