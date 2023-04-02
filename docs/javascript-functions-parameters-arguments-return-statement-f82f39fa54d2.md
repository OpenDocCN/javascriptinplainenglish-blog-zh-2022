# JavaScript 函数—参数和自变量

> 原文：<https://javascript.plainenglish.io/javascript-functions-parameters-arguments-return-statement-f82f39fa54d2?source=collection_archive---------5----------------------->

## 了解视频和动画中的参数、自变量和返回语句。

我们先来了解一下什么是**JavaScript**`Parameter`**&**`Argument`。
也就是`return`的说法是什么。

在上一篇文章中，我们了解了 [*函数的一般概念，函数定义&函数调用*](https://blog.devgenius.io/javascript-functions-explained-a-gentle-intro-part-1-cb6e27595de3) 。如果你想的话，可以去重温一下你的知识。

让我们更深入地了解一下函数。

## 目录:

1.  函数中的 JavaScript 变量
2.  JavaScript 函数—参数和自变量
3.  JavaScript `return` 语句

# 函数中的 JavaScript 变量

JavaScript **函数**也可以**包含变量**。让我们创建一个名为`addNumbers()`的函数来演示一下。

```
function addNumbers() {const **a** = 5;
const **b** = 10;
const **sum = a + b**; // 5 + 10return sum;
}
console.log(addNumbers());
```

## 代码解释:

在功能块`{}`中，我们有 3 个变量`a`、`b`和`sum`，它们都有值。

最后，我们有了`return`关键字。

接着是函数调用，`addNumbers()`

记录函数调用，查看控制台内部的结果。

但是我们可以改变上面的代码，用`Parameters`和`Arguments`来代替变量声明&赋值。

# JavaScript 函数—参数和自变量

JavaScript 函数`parameters`是值的名称(占位符)。

JavaScript 函数`arguments`是参数的实际值。

让我解释给你听，就像我们在街上聊天或者像朋友一样用非正式的语言交谈。

1.  参数是变量名。**参数**这个词只是 JS 里说“**变量名**”**的一个花哨词**
2.  **参数是这些变量的实际值。**自变量**这个词只是“**变量值**”的另一个花哨说法**
3.  **所以我们用参数(变量名)来指代实参(实际变量值)**

**有道理？让我们在代码中看到它，或者更好地将上述函数的变量&它们的值转换成参数&自变量。**

```
function addNumbers(**a, b**) {const sum = **a + b**; // 5 + 10return sum;
}
console.log(addNumbers(**5,** **10**));
```

## ****代码解释:****

**而不是在功能块`{}`里面写变量名。**

**我们将它们写在函数括号`()`中。**

**我们在函数调用`addNumbers(5, 10)`中给出了参数(实际变量值)。**

**大多数人看不到参数&自变量之间的关系(包括我自己)。所以我决定制作一个视频，动画和图片来帮助你形象化。**

**注意，我们不需要在`()`括号内使用 **JavaScript 关键字** `const`、`let` 或`var`来声明变量`a`和`b`。**

# **JavaScript `return` 语句**

**JavaScript `return` 语句听起来像是返回了什么。**

**当 JavaScript 函数到达 return 语句时，它将停止函数执行，并将值返回给调用者。**

***感谢阅读。关注我的* [*Youtube 频道*](https://www.youtube.com/deepspacex)**

***这里也是在培养基上。***

***我爱咖啡，你可以在这里给我买一杯* [*给我买一杯*](https://www.buymeacoffee/deepspacex)**

****更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。****