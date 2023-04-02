# 如何在 JavaScript 的循环中使用 for…of 和 for…

> 原文：<https://javascript.plainenglish.io/using-for-of-and-for-in-loops-in-javascript-a1d531701026?source=collection_archive---------15----------------------->

## 关于在 JavaScript 循环中使用 for…of 和 for…in 的教程。

![](img/dd0f2f18c766b1f3d5909321ea9afbf8.png)

## 介绍

在 ES6 之前，如果我们想遍历一些数据，比如数组，我们可以使用 for 循环。这对我们来说仍然是一个不错的选择，但是从 ES6 开始，我们有了一些额外的选择。

当我们迭代任何可迭代的东西时，比如字符串或数组，我们可以使用 for…of 循环。通过使用 for…of 循环，我们避免了每次循环运行时使用索引或增加变量的需要。当我们使用 for…时，变量本身返回元素，而不是索引。让我们看看这个。我们将从使用 for 循环来 console.log 数组中的值开始。

```
const values = [1, 2, 3, 4, 5];for(let i = 0; i < values.length; i++) {
  console.log(values[i]);
}//Returns --->1
2
3
4
5
```

在上面的例子中，我们使用一个名为 *values* 的常量来声明一个变量。我们给它分配一个数组，包含值 1 到 5。接下来，我们使用一个 for 循环，它将 *i* 声明为一个计数器，在循环内部，我们控制台记录 *i* 的值。现在让我们重复同样的例子，但是这次使用 for…of 循环。

```
const values = [1, 2, 3, 4, 5];for(const value of values) {
  console.log(value);
}//Returns --->
1
2
3
4
5
```

这一次，我们在循环中声明了一个名为 *values* 的变量，在循环内部，我们控制台注销了值为*的*变量。我们得到了与使用 for 循环相同的返回值。

## 遍历对象

如果你想遍历一个对象，For…of 循环是不起作用的。如果你想这样做，你应该使用 for…in。让我们来看一个例子。

```
const drinks = { tea: 1, soda: 4, coffee: 5 };
for(const drink in drinks) {
  console.log(drink);
}//Returns --->
tea
soda
coffee
```

在上面的例子中，我们创建了一个对象文字，并将其赋给一个名为 *drinks* 的变量。使用 for…in 循环，我们设置一个名为 *drink* 的变量，并在每次循环运行时控制台记录 *drink* 的值。我们把钥匙印在控制台上。如果我们想打印每个属性的值，我们可以使用方括号。让我们更新代码来显示这一点。

```
const drinks = { tea: 1, soda: 4, coffee: 5 };
for(const drink in drinks) {
  console.log(drinks[drink]);
}//Returns --->
1
4
5
```

这一次我们得到了返回的每个键的值。当在循环中使用 for…of 或 for…时，我们可以在循环中对变量使用 const。这在标准 for 循环中不起作用。我们这样做的原因是每次循环运行时都会创建一个新的作用域。

我希望您喜欢这篇用 JavaScript 创建随机数的介绍。更多内容请关注我。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**