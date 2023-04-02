# 使用程序模板学习 JavaScript:函数模板第 1 部分

> 原文：<https://javascript.plainenglish.io/learning-javascript-using-program-templates-the-function-template-part-1-a572680d5010?source=collection_archive---------25----------------------->

## 如何在 JavaScript 中创建函数，以及如何使用它们使您的程序更容易编写、阅读和调试

![](img/a47a661245de79341326fb845fdec078.png)

Photo by [Max Duzij](https://unsplash.com/@max_duz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

任何程序员可以学习的最重要的技能之一是如何在他们的程序中有效地创建和使用函数。在本文中，我将演示如何在 JavaScript 中创建函数，以及如何使用它们使您的程序更容易编写、阅读和调试。

不像我以前写过的其他特性那样，函数没有特定的程序模板。然而，我仍然需要写一篇关于函数的文章，所以我将向您展示一个定义函数的模板，然后我们将看几个在 JavaScript 程序中使用函数的例子。

# 什么是功能，我们为什么需要它们？

简单地说，函数是 JavaScript 计算的名称。当您想要定义如何计算某个值、如何将数据从一种形式转换为另一种形式，或者当您想要指定一个经常使用的特定编程任务以命名它时，可以使用函数。

使用函数的一个主要原因是使我们的 JavaScript 程序模块化。模块化程序是由函数构成程序主体的程序。当你看到一些例子时，这将更有意义。

使用函数的另一个原因是它们使你的程序更容易阅读。通过将你的程序主要由函数组成，阅读你的程序的人可以浏览这些函数并决定他们是否需要阅读函数定义的细节。这被称为抽象，是计算机编程中的一项关键技能。

函数也使你的程序更容易调试。当您的程序仅由很长的 JavaScript 代码组成时，很难知道程序中的错误发生在哪里。当您的程序主要由函数组成，而其中一个函数不能正常工作时，您可以将注意力集中在该函数的定义上。否则，您会发现自己在一行又一行的代码中试图确定哪一行出错了。

出于所有这些原因，您应该致力于编写主要由函数调用组成的 JavaScript 程序。现在让我们看看如何在 JavaScript 中定义和使用函数。

# 定义函数

函数有一个模板，您可以学习它来简化新函数的定义。下面是用 JavaScript 定义函数的语法模板:

```
function function-name(parameter list) {
 function-body;
 return statement;
}
```

关于这个模板，我需要说一些事情。首先，参数列表是传递给函数的一组数据。函数最常见的用途之一是将数据从一种事物转换成另一种事物。例如，将摄氏温度转换为华氏温度的温度转换函数会将摄氏温度作为参数。

函数体是执行任何数据转换所必需的代码。这可以由一行代码或多行代码组成。

最后，大多数函数都有一个*返回语句*。这是函数将转换后的数据发送回程序的地方。

这让我想到了使用函数的另一部分——函数调用的*。函数调用是程序中调用函数的地方。对返回值的函数的函数调用可以放在任何需要表达式的地方。我将在下面给出的许多例子中演示这一点。*

实际上，让我们从一些例子开始，不再赘言。既然我提到了将摄氏温度转换为华氏温度，让我们从那个确切的例子开始。首先我们需要知道这个换算的公式，就是:(9.0 / 5.0) *摄氏度-温度+ 32.0。

有了这个公式，我们现在可以写出一个函数定义:

```
function ctof(celsius) {
  let fahr = (9.0 / 5.0) * celsius + 32.0;
  return fahr;
}
```

现在让我们在一个程序中使用函数，要求用户输入摄氏温度，函数将温度转换为华氏温度。以下是完整的程序:

```
function ctof(celsius) {
  let fahr = (9.0 / 5.0) * celsius + 32.0;
  return fahr;
}putstr("Enter a Celsius temperature: ");
let celsius = parseInt(readline());
let fahr = ctof(celsius);
print(celsius,"Celsius equals",fahr, "Fahrenheit");
```

以下是该程序两次运行的输出:

```
C:\js>js test.js
Enter a Celsius temperature: 100
100 Celsius equals 212 FahrenheitC:\js>js test.js
Enter a Celsius temperature: 0
0 Celsius equals 32 Fahrenheit
```

这里，函数调用用于返回分配给变量的值。但是由于函数调用可以放在任何需要表达式的地方，我们也可以只显示函数调用的返回值。

为了演示这一点，让我们创建另一个函数，它只取一个数并对其求平方。定义如下:

```
function square(number) {
  let squared = number * number;
  return squared;
}
```

这个定义是可行的，但是我们真的不需要麻烦地将平方值赋给一个变量，然后返回这个变量。相反，由于我们想从函数中得到的只是它的返回值，所以我们可以立即将函数的平方值返回给调用程序。

这是新的定义:

```
function square(number) {
  return number * number;
}
```

下面是一个使用该函数的程序:

```
function square(number) {
  return number * number;
}putstr("Enter a number: ");
let num = parseInt(readline());
print(num,"squared is",square(num));
```

以下是该程序几次运行的输出:

```
C:\js>js test.js
Enter a number: 2
2 squared is 4C:\js>js test.js
Enter a number: 12
12 squared is 144C:\js>js test.js
Enter a number: 2.25
2 squared is 4
```

最后一个例子返回了一个整数值，因为我使用了`parseIn` t 来转换字符串输入。对于处理数字的程序，你可能想使用`parseFloat`来确保没有数据丢失。

函数调用也可以在另一个函数定义中使用。例如，我们可以编写一个计算两个平方值之和的函数，如下所示:

```
function sum_of_squares(num1, num2) {
  return square(num1) + square(num2);
}
```

下面是一个使用该函数的简短程序:

```
putstr("Enter first number: ");
let num1 = parseFloat(readline());
putstr("Enter second number: ");
let num2 = parseFloat(readline());
let sumSquares = sum_of_squares(num1, num2);
print("Sum of squares of",num1,"and",num2,"is:",sumSquares);
```

这个程序运行一次的输出是:

```
C:\js>js test.jsEnter first number: 2Enter second number: 3Sum of squares of 2 and 3 is: 13
```

# 多参数函数

对于最后一个例子，让我们看几个需要多个参数的函数定义。我将使用的示例是一个计算直线上两点之间距离的函数。以下是计算该值的公式:

```
d = √[(x2 − x1)2 + (y2 − y1)2]
```

该函数的参数将是这两个点的 x 和 y 值。下面是这个函数的定义以及一个测试它的程序:

```
function distance(x1, y1, x2, y2) {
  let dx = x2-x1;
  let dy = y2-y1;
  let dsquared = dx * dx + dy * dy;
  return Math.sqrt(dsquared);
}putstr("Enter x of first point: ");
let x1 = parseInt(readline());
putstr("Enter y of first point: ");
let y1 = parseInt(readline());
putstr("Enter x of second point: ");
let x2 = parseInt(readline());
putstr("Enter y of second point: ");
let y2 = parseInt(readline());
let dist = distance(x1, y1, x2, y2);
print("The distance is", dist);
```

下面是这个程序运行一次的输出:

```
Enter x of first point: 1
Enter y of first point: 2
Enter x of second point: 4
Enter y of second point: 3
The distance is 3.1622776601683795
```

# 最后的想法

创建和使用函数是学习成为一名高效程序员的重要部分。在本文中，我演示了如何创建返回值的函数，这是大多数 JavaScript 程序中最常用的函数类型。

在我的下一篇文章中，我将讨论如何创建和使用严格用于它们执行的代码的函数。在一些语言中，这些类型的函数被称为 void 函数，一些编程语言称它们为过程，我将用这个术语来描述它们。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。**