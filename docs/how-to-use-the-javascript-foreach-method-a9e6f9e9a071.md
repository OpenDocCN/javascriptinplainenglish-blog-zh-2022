# 如何使用 JavaScript forEach()方法

> 原文：<https://javascript.plainenglish.io/how-to-use-the-javascript-foreach-method-a9e6f9e9a071?source=collection_archive---------14----------------------->

## 了解如何使用数组帮助器方法 forEach()。

![](img/80b829f1a5907eba447e8847ca9ef045.png)

## 数组助手方法

JavaScript 有一个在 ES6 中引入的数组助手方法集合。如果您熟悉诸如下划线或 Loadash 之类的库，那么您可能已经熟悉了这些方法。在 ES6 中，这些被引入到语言中。数组助手方法帮助我们操作和处理存储在数组中的数据。本文将介绍其中的一种方法 forEach()。

## forEach()简介

forEach()对数组中的每个元素调用一次函数。该方法接受以下参数:

*   将对数组中的每个元素执行的回调函数。
*   当前正在使用的单个元素。
*   当前元素的索引。
*   调用 forEach 的数组。
*   thisArg 是一个可选参数，允许您在执行回调函数时访问要用作 this 的值。

让我们从使用 forEach()的一个非常基本的例子开始。

```
const ourNumbers = [5, 4, 3, 2, 1];ourNumbers.forEach(function (number) {
  console.log(number)
});//Returns ---> 
5
4
3
2
1 
```

在上面的例子中，我们用 const 声明了一个变量，我们给它赋予了标识符*和编号*。然后我们用一个包含一些数字的数组来初始化它。接下来，我们使用 forEach()方法。我们在 *ourNumbers* 数组上调用 forEach()。在方法的参数中，我们传递一个匿名函数。我们可以将匿名函数参数命名为我们想要的任何名称，但是它代表的是单个元素。我们把例子中的参数称为*号*。在函数体中，我们 console.log 了*号*参数的值。当代码运行时，我们从打印到屏幕上的 *ourNumbers* 数组中获取每个元素。

因此，在继续之前，让我们回顾几点。当我们使用 forEach()时，该方法接受的回调函数会被使用 forEach()方法的数组中的每个元素调用一次。通常，为回调使用匿名函数(传递给方法的函数)是有意义的，因为代码不会被重用。如果我们愿意，我们可以给这个方法传递一个命名函数。让我们看看我们将如何做到这一点。

```
const ourNumbers = [5, 4, 3, 2, 1];function printNumber(number) {
  console.log(number);
}ourNumbers.forEach(printNumber);//Returns --->
5
4
3
2
1
```

在上面的示例中，我们的代码与前面的示例相同，只是这次我们没有使用匿名函数，而是将对该函数的引用传递给 forEach()。注意，当你像这样传递函数时，不要用括号。

## 循环呢？

通过使用一个循环，我们可以获得与上面例子中相同的结果。我们来对比一些例子。

```
const ourNumbers = [5, 4, 3, 2, 1];for(let i = 0; i < ourNumbers.length; i++) {
 console.log(ourNumbers[i]);
}//Returns --->
5
4
3
2
1const ourNumbers = [5, 4, 3, 2, 1];for(let nums of ourNumbers) {
  console.log(nums)
}//Returns --->
5
4
3
2
1
```

使用 for 循环和 for of 循环提供的输出与使用 forEach()相同。使用哪种方法的选择实际上取决于您想要实现的目标，但是使用 forEach()通常不太容易出错，因为您需要担心的设置较少。经常使用 forEach()也更具可读性。

## 其他示例

让我们再看几个使用 forEach()的例子。

```
const ourNumbers = [5, 4, 3, 2, 1];ourNumbers.forEach(function (number) {
  console.log(number + 1)
});//Returns ---> 
6
5
4
3
2
```

在上面的例子中，我们使用了相同的数组和设置，但是这次我们给每个元素增加了一个。如果我们想访问元素的索引，我们可以在数字后面传入另一个参数。

```
const ourNumbers = [5, 4, 3, 2, 1];ourNumbers.forEach(function (number, index) {
  console.log(number, index)
});//Returns ---> 
5 0
4 1
3 2
2 3
1 4
```

也许我们想得到 *ourNumbers* 数组的总和。使用 forEach()我们可以通过以下示例实现这一点:

```
const ourNumbers = [5, 4, 3, 2, 1];let sum = 0;ourNumbers.forEach(function (number) {
  sum += number;
});console.log(sum);
//Returns ---> 15
```

在上面的例子中，在我们创建了 *ourNumbers* 数组之后，我们创建了一个名为 *sum* 的变量，我们用零值对其进行初始化。我们可以认为这有点像一个追踪器，当每个元素被合计时，它将保存我们的元素的运行总数。在 forEach()内部，我们将数字(当前元素)添加到 *sum* 中。然后我们`console.log`计算 *sum* 的总和，这是所有 *ourNumbers* 数组元素加在一起的总和。

## 嵌套数据结构

当我们处理嵌套数据时，forEach()特别有用。让我们看一个例子:

```
const students = [
{
  name: "Anna",
  age: 50
},
{
  name: "Pete",
  age: 20
},
{
  name: "Abby",
  age: 12
  }
];students.forEach(function(student) {
  console.log(student.name.toUpperCase())
})//Returns --->
ANNA
PETE
ABBY
```

在上面的例子中，我们使用一个名为 *students* 的常量来声明一个变量。我们用一个包含三个对象的数组来初始化它。每个对象包含我们学生的姓名和年龄。然后我们使用 forEach()访问每个对象的*名*，并使用 toUpperCase()方法访问每个*名*的`console.log`名*名*。当代码运行时，我们将每个 *name* 值大写并打印到屏幕上。

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*