# 使用程序模板学习 JavaScript:函数高级特性介绍

> 原文：<https://javascript.plainenglish.io/learn-javascript-with-program-templates-an-introduction-to-the-advanced-features-of-functions-be19364dd859?source=collection_archive---------22----------------------->

## 高效编程函数的一些高级特性介绍。

![](img/0db6e78d5f6e698a06cf7e76bc95b377.png)

Photo by [Lagos Techie](https://unsplash.com/@heylagostechie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我回到通过程序模板学习 JavaScript 之前，我还有一篇关于函数的文章要写。在本文中，我将向您介绍一些函数的高级特性，这些特性可以帮助您使您的程序更易于阅读、调试和提高效率。让我们开始吧。

# 参数对象

每次创建函数时，都会创建一个名为`arguments`的内置对象。这个对象是一个数组，它的元素是你提供给函数的参数。使用这个对象，即使函数定义只有一个参数，也可以调用具有不同数量参数的函数。

让我们通过一个例子来看看这是如何工作的。下面的函数允许用户输入不同数量的参数(数字)，函数计算并返回所有参数的总和。下面是函数定义和使用该函数的一个简短程序:

```
function sum(numbers) {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}print(sum(1,2,3));
print(sum(1,2,3,4,5,6,7,8,9,10));
```

这个程序的输出是:

6
55

您应该注意到 arguments 对象类似于数组，但不是真正的 JavaScript 数组。

# 默认参数

有时，您希望函数为用户提供一个默认参数，在调用函数时使用该参数，而在函数调用中不使用该参数。以这种方式定义的参数被称为*默认参数*。

让我们检查默认参数的一种用法。下面的函数返回雇员的工资总额，忽略任何扣减。这两个参数是工资率和工作时间。在这家公司，大多数员工每周工作 40 小时，所以我们可以使用 40 作为计算薪水的默认参数。

下面是函数定义和一个演示如何使用该函数的小程序:

```
function grossPay(rate, hours = 40.0) {
  return rate * hours;
}let rate1 = 23.00;
print("Gross pay for 40 hours is:", grossPay(rate1));
let rate2 = 33.10;
let hours1 = 35;
print("Gross pay for 35 hours is:",grossPay(rate2, hours1));
```

在第一个`print`语句中，因为工作的小时数是 40，所以省略了第二个参数，让默认值用于计算。在第二个`print`语句中，调用了第二个参数，覆盖了默认值。

这里有一个警告—默认参数需要是参数列表中的最后一个参数。如果不是这样，您的代码将产生不好的结果，尽管它不会导致错误。

为了演示这一点，我重写了`grossPay`函数，将默认参数放在第二个参数之前。下面是函数定义和一个简短的程序:

```
function grossPay(hours = 40.0, rate) {
  return rate * hours;
}print(grossPay(23));
print(grossPay(23, 39));
```

这个程序的输出是:

```
NaN
897
```

让我们通过修改函数定义来显示函数内部的参数，从而进一步研究这一点:

```
function grossPay(hours = 40.0, rate) {
  print("hours, rate:", hours, rate)
  return rate * hours;
}print(grossPay(23));
print(grossPay(23, 39));
```

以下是输出:

```
hours, rate: 23 undefined
NaN
hours, rate: 23 39
897
```

通过将缺省参数放在第一位，导致函数输出值 NaN(不是数字),这是无效的输出。这里的寓意是始终将默认参数作为参数列表中的最后一个参数。

# 休息参数

另一种编写参数数量可变的函数的方法是将一个参数设为 *rest* 参数。休止符参数通过在参数名称前放置三个点来表示。以下是带有 rest 参数的定义的函数模板:

*函数 func-name(…rest-parameter) {
函数体；
}*

当您使用 rest 参数编写函数时，rest 参数被实现为一个数组，您可以像访问标准数组一样访问该数组。下面是一个例子，我们使用 rest 参数代替 arguments 对象重写了前面的`sum`函数:

```
function sum(...numbers) {
  let total = 0;
  for (let i = 0; i < numbers.length; i++) {
    total += numbers[i];
  }
  return total;
}print(sum(1,2,3,4,5,6,7,8,9,10)); // displays 55
```

使用 rest 参数比使用 arguments 对象更容易理解，但是它们的执行方式是一样的。

# 扩展运算符

与 rest 参数类似的是*扩展运算符*。spread 运算符允许您将数组指定为参数，数组的每个元素都作为参数传递给另一个函数调用或运算符。spread 运算符不在参数列表中使用，而是在函数体中使用。

在第一个例子中，一个分数数组被传递给函数`Math.max`，数组中最高的分数被返回:

```
function maxGrade(grades) {
  return Math.max(...grades);
}let grades = [81, 77, 82, 79, 92, 88];
print("Highest grade:", maxGrade(grades));
```

输出是:

```
Highest grade: 92
```

您还可以提供一个外部值以及要展开的数组。这里有一个例子:

```
function maxGrade(grades) {
  return Math.max(...grades, 99);
}let grades = [81, 77, 82, 79, 92, 88];
print("Highest grade:", maxGrade(grades));
```

这里的输出是:

```
Highest grade: 99
```

因为外部的值是最大的值，包括数组内部的值。

# 箭头功能

我将以对*箭头功能*的简短讨论来结束本文。箭头函数，有时也称为粗箭头函数，不需要使用 function 关键字，而是让您将函数定义赋给变量。您还可以使用箭头函数来定义匿名函数，以便与数组函数(如 every)一起使用。

arrow 函数还有其他更技术性的特性，但是现在我将集中讨论这个简单的用法。

将箭头函数分配给变量的语法模板是:

*设 var-name = (parameter-list) = >函数体；*

下面的示例分配一个函数定义，该函数定义将其参数平方为一个变量。代码如下:

```
let square = (x) => x * x;
print(square(2)); // displays 4
```

下面是一个带有两个参数的示例:

```
let power =
  (base, exp) => {let product = 1;
    for (let i = 1; i <= exp; i++) {
      product *= base;
    }
    return product;
  }print(power(2,3)); // displays 8
```

您也可以使用箭头函数来定义匿名函数，作为另一个函数调用的一部分来调用。例如，数组函数映射将函数应用于数组的每个元素。函数映射调用可以是数组函数。

下面是一个例子，其中数组的每个元素都是平方的:

```
let nums = [1,2,3,4,5];
let numsquared = nums.map(x => x * x);
print(numsquared);
```

输出是:

```
1,4,9,16,25
```

箭头函数的内容比我在这里展示的要多得多，但是这些主题需要留待更高级的文章来讨论。

# 最后的想法

函数是每种编程语言的重要组成部分，你应该花额外的时间来掌握它们。在本文中，我强调了 JavaScript 函数的一些额外特性，您可以利用这些特性使您的程序变得更好。

请回复这篇文章或发邮件给我，告诉我你的意见和建议。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*