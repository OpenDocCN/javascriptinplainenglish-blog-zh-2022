# JavaScript 循环/循环代码- JavaScript 学习之旅

> 原文：<https://javascript.plainenglish.io/javascript-loops-looping-code-javascript-learning-journey-330801acc2ef?source=collection_archive---------12----------------------->

# 第十二课

![](img/8fd12045044a8fad9f4c0be0ff4d45f6.png)

“Colourful Loops!” Photo by [Etienne Girardet](https://unsplash.com/@etiennegirardet?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从上一课——第 11 课——JavaScript 数组开始，可以通过下面的链接找到，我们简要地提到了可以在数组上执行的循环。本课将深入探讨循环，各种类型的循环以及如何使用它们。下面是关于数组的最后一课，以防你错过…

[](https://medium.com/@m_sally/javascript-arrays-javascript-learning-journey-f59f0d08df4b) [## JavaScript 数组— JavaScript 学习之旅

### 第 11 课 JavaScript 中的数组是什么，数组为什么/如何有用

medium.com](https://medium.com/@m_sally/javascript-arrays-javascript-learning-journey-f59f0d08df4b) 

# 环

循环是有用的编码语言工具，可以用少量代码执行重复的任务，并且可以被计算机非常快速地处理。在 JavaScript 中，循环是一种重复一组指令直到满足特定条件的方式。循环用于多次执行同一代码块。当您想要对大量项目执行相同的操作时，这很有用，例如当您想要迭代数组中的元素并对每个元素执行相同的操作时，例如计算。循环是 JavaScript 编程的重要组成部分，它们被广泛应用于各种应用程序中，你甚至可以使用循环来记录用户点击网页上某个按钮的次数。一般来说，循环是自动执行代码中重复任务的一种有用的方式，可以提高代码的效率并节省时间。

JavaScript 中有几种不同类型的循环，但最常用的是`**for**`循环和`**while**`循环。以下是所有可用的循环类型。

## 循环的类型

JavaScript 中有几种类型的循环，每种循环都有不同的用途，并通过关键字进行操作:

*   `**for**`
*   `**for … in**`
*   `**for … of**`
*   `**forEach()**`
*   `**while**`
*   `**do … while**`
*   `**map()**`

`**FOR**` **循环**

最基本的循环类型是`**for**`循环，用于迭代一组项目，并指定一个条件来确定循环将运行多少次。一个`for`循环有 3 个部分:一个开始条件，一个停止/结束条件，以及一个决定循环变量如何在循环的每次迭代中更新的步骤。

`**for**`循环的基本语法是:

```
for (initialisation; stop condition; update){
  instruction code to be executed
}
```

`**for**`循环的初始化部分为计数器变量设置一个起始值(由下面例子中的`i`指定的变量)。该条件是一个布尔表达式，在循环的每次迭代之前进行检查，如果条件为' **true'** ，则执行循环内的代码。然后，update 的最终表达式在每次迭代结束时执行，用于更新计数器变量，并指定循环每次运行时应如何更新。如果条件为**假**，循环结束。每次迭代后，增量/减量用于更新循环变量。

一个`**for**`循环的例子:

```
for (let i = 1; i <= 5; i++){
  console.log(i); 
}
```

上面的循环示例在您的控制台中记录数字 1 到 5。循环从 1 开始，一直运行到`i`不再小于或等于 5。每次循环运行时,`i`将增加 1。控制台中的结果将显示以下内容:

```
1
2
3
4
5
```

`**WHILE**` **循环**

`**while**`循环类似于`for`循环，但没有初始化、条件和更新的表达式——最终表达式部分。相反，`**while**`循环只有条件，只要条件为'**真**'，循环内部的代码就被执行，次数可以是未知的。重要的是要确保条件最终会变为假，否则循环将永远运行(也称为“无限循环”)，并可能使您的计算机崩溃。

`while`循环的基本语法是:

```
while (stop condition) {
  code to be executed 
}
```

与上面的`for`循环做同样事情的`while`循环的例子:

```
let i = 1;
while (i <= 5) {
  console.log(i);
}
```

从上面的例子中可以看出，`for`循环和`while`循环都可以用来完成类似的任务，但是它们在不同的情况下使用，这取决于你是否预先知道你想要重复代码多少次。

`**DO ... WHILE**` **循环**

`**do-while**`循环，类似于`**while**`循环，但是有一个关键的区别:在检查条件之前，无论条件如何，循环中的代码块至少执行一次。一个`**do-while**`循环的例子:

```
let i = 1;
do {
  console.log(i); i++; 
} while (i <= 5);
```

上面的循环示例还将在控制台中打印数字 1 到 5。

`**FOR ... IN**` **循环**

`**for-in**`循环用于遍历一个对象的属性。它们通常用于遍历对象的键，但也可以用于遍历值。

例如:

```
let object = {a: 1, b: 2, c: 3}; 
for (let key in object) { 
  console.log(key + ": " + object[key]); 
}
```

这个循环将打印出对象变量的属性(a，b，c)和它们的值(1，2，3)。控制台将显示以下内容:

```
a: 1
b: 2
c: 3
```

另一个例子:

```
let person = { name: "Adam", age: 25, job: "teacher" }; 
for (let key in person) { 
  console.log(key + ": " + person[key]); 
}
```

这个循环将遍历 person 对象中的每个属性，并打印出键和值。输出将是:

```
name: Adam
age: 25
job: teacher
```

`**FOR ... OF**` **循环**

`**for-of**`循环用于遍历一个可迭代对象中的值，比如一个数组。它们类似于`for-in`循环，但是它们只循环值而不循环键。一个`for-of`循环的例子:

```
let numbers = [1, 2, 3, 4, 5]; 
for (let number of numbers) {
  console.log(number); 
}
```

这个循环将遍历 numbers 数组中的每个值，并在控制台中打印 1 到 5。输出将是:

```
1 2 3 4 5
```

`**FOR EACH**` **循环**

`forEach()`循环是一种用于迭代数组元素并对数组中的每个元素执行函数的方法。`forEach`循环是使用传统`for`循环的一种方便的替代方法。该方法通常用于对数组中的所有元素执行一些操作，例如对每个元素应用一个函数来计算每个元素的新值，或者向 DOM 元素数组中的每个元素添加事件侦听器。

例如，您可以使用 forEach 循环遍历数组的元素，并将每个元素打印到控制台:

```
const array = [1, 2, 3, 4, 5];
array.forEach(element => {
  console.log(element);
});

// Also can be written as..
let numbers = [1, 2, 3, 4, 5]; 
numbers.forEach(function(number) {
  console.log(number); 
});
```

这段代码将数字 1 到 5 打印到控制台，每行一个数字，如上面的`for`循环示例所示。`forEach`循环是遍历数组元素并对每个元素执行操作的一种便捷方式，无需使用传统的 for 循环。它类似于一个`for`循环，据说更容易使用和更有效，因为`forEach()`没有使用计数器来跟踪数组中的当前元素，而是将元素直接传递给回调函数。

`**MAP()**`

`map()`方法不是传统意义上的循环，但它的行为确实像一个循环，因为它遍历数组中的元素，并通过对每个元素应用一个函数来操作数组中的每个元素，然后返回一个包含已转换元素的新数组。动作可以保存到存储函数结果的新数组名称中。

使用`**map()**`转换数组中元素的例子:

```
let numbers = [1, 2, 3];
let doubledNumbers = numbers.map(number => number * 2);
console.log(doubledNumbers);
```

在本例中，`**map()**`遍历`**numbers**`数组中的元素，并将提供的函数(`**number => number * 2**`)应用于每个元素。返回值用于在`**doubledNumbers**`数组中创建一个新元素。在您的控制台中，示例代码的输出将是[2，4，6]。

注意:在后面的课程中，会有更多关于函数和箭头函数的内容，如上面的一些示例代码所示。`**map()**`是一个高阶函数，这意味着它将一个函数作为参数，并返回一个新函数。为数组中的每个元素调用提供的函数，返回值用于在结果数组中创建一个新元素。

虽然`map()`可能不被认为是一个循环，但它执行类似的功能，在某些情况下可作为循环的替代。`**map()**`据说以一种比传统循环更有效的方式实现。它为处理数组进行了优化，不需要您自己编写循环代码。这可以让你的代码更简洁，更易读。

所有这些循环都是 JavaScript 中重复动作的有用工具，它们可以在各种情况下使用，通过节省编写重复代码的时间来提高代码的效率。为任务选择正确的循环并小心使用循环很重要，因为如果不小心，很容易创建无限循环(永不停止的循环)，这可能会使您的计算机崩溃。确保循环最终会结束，方法是始终包含一个退出循环的方法，要么递增计数器，要么以其他方式改变条件。

## 参考

一些有用的资源，包括一些用作本文参考点的资源，包括:

[w3 学校](https://www.w3schools.com/)

[MDN 网络文档](https://developer.mozilla.org/)

[javascript.info](https://javascript.info/) 网站

这些资源(带有其网站的链接)提供了对 JavaScript 以及其他语言(包括 HTML、CSS 等)的进一步深入研究，以帮助您探索 Web 开发的编码之旅。他们也向你展示了如何用信息和练习来帮助你进行编码。莎莉·M

希望您喜欢这一课，并学到了一些关于 JavaScript 循环的新信息。

期待在下一课中见到您——第 13 课，了解更多 JavaScript 基础知识。

![](img/e84927f823e9bc9f182b805b53b1ae9a.png)

*Sally M——本故事中的所有文字和图片均属于作者——Sally M(除非另有注明)。这种作品受版权法保护。作者 Sally M 花了很多时间写这篇文章。由于使用媒体的人侵犯了版权，作者添加了这段文字。本文最后更新:2022 年 12 月 16 日。*

如果你喜欢这些课程，请注意，你可以捐赠给作家的教学互联网基金事业继续这些课程和其他伟大的作品。查看下面的*“奖励作家”*细节。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****