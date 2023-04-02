# JavaScript 中的数组析构

> 原文：<https://javascript.plainenglish.io/array-destructuring-in-javascript-c79b747dd864?source=collection_archive---------12----------------------->

## 了解如何使用数组析构编写更简洁的代码

![](img/aca2540ac494313636d7fe1f06b2f521.png)

## 什么是解构？

想象一下，你去一家超市，你挑选一些商品，然后把它们装进袋子里。当你一个接一个回家时，你打开这些东西并把它们放好。

当我们编写代码时，我们可以使用析构作为一种方法，从数据结构(如对象和数组)中解包或挑选出某些元素项，然后将这些值放入它们自己的独立变量中。

## ES6 之前

在 ES6 之前，如果我们想从数据结构(比如数组)中挑选出某些元素，我们必须使用元素的索引，然后将其保存到变量中。让我们来看看我们将如何处理这个问题。

```
var days = [
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
  "Sunday"
];var first = days[0];
var second = days[1];
var third = days[2];console.log(first, "First");
console.log(second, "Second");
console.log(third, "Third");//Returns --->
Monday First
Tuesday Second
Wednesday Third
```

在上面的例子中，我们首先声明一个名为 *days* 的变量。我们将一个数组赋给变量，在数组中我们存储了一周中每一天的字符串。接下来，我们声明三个变量，*第一个* , *第二个*和*第三个*。在每个变量中，我们通过使用元素的索引来存储来自 *days* 数组的前三个元素。最后，我们控制台. log 出第一个、*、第二个*和第三个变量的值。我们得到了打印在屏幕上的 *days* 数组的前三个元素的字符串。

虽然这种方法可行，但有一种更简单的方法来解决这个问题，那就是使用数组析构。

## ES6 阵列销毁

使用析构，我们可以在一行代码中挑选出所需的元素。

```
const ourArray = [1, 2];
const [itemOne, itemTwo] = arrayName;
```

为此，我们创建了一个数组，并在数组内部放置了我们希望用来命名要赋值的元素的变量的名称。接下来，我们使用等号运算符和您希望从中选取元素的数组的名称。然后使用等号运算符和希望从中重构元素的数组的名称。数组中的变量将根据元素的位置设置为初始数组中元素的等效值。

让我们看看最初的例子，但是这次使用了析构。

```
var days = [
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
  "Sunday"
];const [first, second, third] = days;console.log(first, "First");
console.log(second, "Second");
console.log(third, "Third");//Returns --->
Monday First
Tuesday Second
Wednesday Third
```

## 析构的附加特征

析构也允许我们通过使用逗号来跳过一个索引。如果我们想从 *days* 数组中挑选出第一、第二和第四个元素，我们将使用这种方法。

```
var days = [
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
  "Sunday"
];const [first, second, , fourth] = days;console.log(first, "First");
console.log(second, "Second");
console.log(fourth, "Fourth");//Returns --->
Monday First
Tuesday Second
Thursday Fourth
```

我们还可以使用 rest 操作符将数组中剩余的值收集到一个变量中。

```
var days = [
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
  "Sunday"
];const [first, ...remainingDays] = days;console.log(first, "First");
console.log(remainingDays, "Remaining");//Returns --->
Monday First
(6) ['Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']0: "Tuesday"1: "Wednesday"2: "Thursday"3: "Friday"4: "Saturday"5: "Sunday"length: 6[[Prototype]]: Array(0) 'Remaining'
```

我希望你喜欢这篇文章，你可以在这里看一个视频:

请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**