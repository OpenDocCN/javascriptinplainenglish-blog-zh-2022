# 简化的数组析构

> 原文：<https://javascript.plainenglish.io/array-destructuring-simplified-10300505499?source=collection_archive---------10----------------------->

## 如何使用析构的初学者指南？

![](img/d4a08184849056970a21c1f64518fafd.png)

Photo by [Marcello Gennari](https://unsplash.com/@marcello54?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

析构是 ES6 中引入的概念，它有助于以更有效的方式为复杂数据类型分配变量。

在这个讨论中，我们将看到一个关于如何使用析构的简要介绍。我们将把它分成三个部分，分别是数组、对象和函数的析构。

但在此之前，让我们先了解一下什么是析构。

```
let num = 5;
```

在上面的代码片段中，我们构造了一个变量 ***num*** ，它的值为 5。析构的工作与结构化相反，在结构化中，我们分解一个数据结构，并将这些单独的值赋给特定的变量。

**听起来令人困惑？**没问题，当我们开始用单独的数据类型来处理它们时就清楚了。

那我们开始吧！

1.  **基本用法**

```
let arr = [1, 2, 3];   // Array Declaration  - (1)const [a, b] = arr;   // Destructuring of Array - (2)console.log(a);   1console.log(b);  2
```

在上面的例子中，在步骤 2 中，我们析构了创建的数组(arr)。它的意思是，我们打开所有的值，并按顺序把这些值赋给左边运算符中定义的变量。
因为我们只在左侧定义了 2 个变量，所以只将数组的前 2 个值分配给变量 a 和 b。

2.**将数组解构为数组+变量**

我们也可以使用 spread 运算符将数组的一部分移动到另一个数组。例如:

```
let arr = [1, 2, 3, 4, 5, 6];const [a, b, ...c] = arr;console.log(a);   1console.log(b);   2console.log(c);   [3,4,5,6]
```

因此，从上面的例子可以看出，我们分解了数组，将前 2 个值赋给变量，其余的值赋给数组。

3.**数组拼接**

如果我们想用一些拼接的数据创建一个数组，也可以使用析构。

```
let arr = [1, 2, 3, 4, 5, 6];const [, , ...c] = arr;console.log(c);  // [3,4,5,6]
```

在这里，当析构数组时，我们给了 2 个空白字段，这意味着开始的 2 个字段应该被忽略，其余的字段被推入到使用 spread 运算符添加的数组变量中。

4.**给变量**分配特定的索引值

我们还可以使用析构函数获取数组的指定值，并将其赋给一个变量。例如，假设我们想获取第三个值，并将其赋给一个变量。

```
let arr = [1, 2, 3, 4, 5, 6];const [, , c] = arr;console.log(c);  3
```

5.**析构时的默认值**

如果数组长度小于析构时传递的变量参数，我们可以设置一个默认值。

```
let arr = [1, 2];const [a = 2, b = 3, c = 1] = arr;console.log(a); 1console.log(b); 2console.log(c); 1
```

因此，正如我们所观察到的，由于数组的长度只有 2，在析构表达式中，我们给了 3 个属性默认值。如果在右侧表达式中找不到值，则应用默认值。

6.**交换变量**

我们还可以利用析构来交换变量，而不需要使用额外的变量。

```
let a = 1;let b = 2;console.log('Before Swap');console.log('Value of a', a);console.log('Value of b ', b);[b, a] = [a, b];console.log('After Swap');console.log('Value of a', a);console.log('Value of b ', b);Output
Before Swap
Value of a 1
Value of b  2
After Swap
Value of a 2
Value of b  1
```

因此，这里你可以看到我们使用了析构概念，并以相反的方式赋值。

所以，这在坚果壳中是析构的基础，我们试图在数组析构的帮助下理解它。在下一部分，我们将深入了解对象析构是如何工作的。

如果你有任何关于数组析构的疑问，请回复我。

关于我——我是一个编程爱好者，喜欢阅读和写作前端设计、JavaScript 和 UI/UX 相关的东西。点击[这里](https://medium.com/@avinash.dev21987)阅读我所有的文章，并让我知道你的反馈。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*