# JavaScript 数组简介(绝对初学者)

> 原文：<https://javascript.plainenglish.io/javascript-arrays-for-absolute-beginners-b4d750867af7?source=collection_archive---------6----------------------->

如果您计划在简单的`"hello world"`输出之外推进您的 JavaScript 项目，您将需要使用[数组](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)。

在本文中，我们将介绍什么是数组，如何创建数组以及您可以使用它做什么。我们开始吧！

![](img/d4e0c6e0f33170eda5aa8d1f902e7c88.png)

# 什么是数组？

在 JavaScript 中，数组(在其他语言中也称为**列表**或**向量**)是一个**有序的**值列表。**有序**是指每个元素被放置在某一位置(称为索引)。

JavaScript 数组支持的一个关键特性是，您可以在同一个数组中**存储不同类型的数据(稍后将详细介绍)。例如:同一数组中可以有`String`、`Boolean`和`Number`元素。此外，数组是动态调整大小的**，所以您永远不必手动增加数组的大小。****

**在其他语言中，例如 C 语言，您只能在数组中存储相同类型的数据，并且在创建数组时必须知道数组的大小。**

**现在让我们看看一些代码！**

# **如何创建数组？**

**我们可以用两种不同的方式创建数组；使用**数组文字符号**或`Array()` **构造函数**。**

**创建数组最常见(也是**推荐的**)的方法是使用数组文字符号。**

```
const fruits = [];
```

**这将创建空的`fruits`阵列。**

**您也可以创建一个已经包含元素的数组。**

```
const fruits = ["apple", "pear", "banana"];
```

**不太常见的方法是使用`Array()`构造函数。**

```
const fruits = new Array();
```

**这会创建一个新的空`fruits`数组。**

```
const fruits = new Array(10);
```

**该数组由 10 个`undefined`元素初始化。**

**创建一个已经包含元素的数组也是可能的。**

```
const fruits = new Array("apple", "pear", "banana");
```

**您很可能发现自己从未或很少使用`Array()`构造函数。**

# **我可以在 JavaScript 数组中存储哪些类型的元素？**

**在 JavaScript 中，您可以在数组中存储任何类型的元素，甚至可以混合类型。**

```
const fruits = ["apple", 2, "pear", true, false, ["another", "array", 99]];
```

**这会很快变得混乱，所以我强烈建议您每个数组使用**一个元素类型**！**

**为什么会这样？如果您刚刚开始学习编程或 JavaScript，了解这一点并不重要，所以请随意跳过这一部分。**

**JavaScript 是[动态类型化的](https://developer.mozilla.org/en-US/docs/Glossary/Dynamic_typing)，这意味着变量在**运行时**被赋予其类型。与其他[静态类型](https://developer.mozilla.org/en-US/docs/Glossary/Static_typing)的编程语言相比，后者的变量类型是在**编译时**分配的。**

**换句话说，**动态类型语言**在运行代码后检查类型**，而**静态类型语言在运行代码**前检查类型**。**

# **如何读取一个数组的元素？**

**记住，JavaScript 中的数组是按**排序的**，其中数组中的每个位置都由一个数字表示。这个数字通常被称为**指数**。在 JavaScript 中，数组是从零开始索引的，这意味着列表的第一个元素的索引是 0，第二个元素的索引是 1，依此类推。**

**如果您知道想要读取的元素的索引，您可以简单地这样做**

```
array[index]
```

**让我们看一些实际的代码:**

```
const fruits = ["apple", "pear", "banana"];console.log(fruits[0]);  // "apple"
console.log(fruits[1]);  // "pear"
console.log(fruits[2]);  // "banana"
```

# **如何更新数组中的值？**

**在 JavaScript 中，数组[是可变的](https://developer.mozilla.org/en-US/docs/Glossary/Mutable)，这意味着它们即使在创建后也可以更新。与[不可变的](https://developer.mozilla.org/en-US/docs/Glossary/Immutable)类型相比，例如原始类型`String`和`Number`。**

**让我们看看如何将`fruits`数组中的`apple`更新为`orange`。**

```
const fruits = ["apple", "pear", "banana"];console.log(fruits[0]);  // "apple"// overwrite the element at index 0 with the value "orange"
fruits[0] = "orange";console.log(fruits[0]);  // "orange"
```

**接下来，我们将看看如何执行诸如迭代、添加更多元素等操作。**

# **如何对数组进行基本操作？**

**从哪里开始？您可以对数组进行许多操作。本节涵盖了最有用的操作。**

## **在开头添加一个元素**

**为了给开头添加一个元素，我们使用`unshift()`。**

```
const fruits = ["apple", "pear", "banana"];fruits.unshift("orange");console.log(fruits);
// ['orange', 'apple', 'pear', 'banana']
```

## **在末尾添加一个元素**

**我们使用`push()`将一个元素添加到数组的末尾。**

```
const fruits = ["apple", "pear", "banana"];fruits.push("orange");console.log(fruits);
// ["apple", "pear", "banana", "orange"]
```

## **从头删除一个元素**

**我们使用`shift()`从数组的开始移除一个元素。这个方法做两件事:返回“移位”的元素并将其从数组中移除。**

```
const fruits = ["apple", "pear", "banana"];const poppedFruit = fruits.pop();console.log(poppedFruit); // "apple"console.log(fruits);
// ["pear", "banana"];
```

## **从末端移除元素**

**我们使用`pop()`从数组中“弹出”最后一个元素。这做了两件事:返回“弹出”的元素并将其从数组中移除。**

```
const fruits = ["apple", "pear", "banana"];const poppedFruit = fruits.pop();console.log(poppedFruit); // "banana"console.log(fruits);
// ["apple", "pear"];
```

## **删除特定元素**

**有许多方法可以做到这一点(就像编程中的许多事情一样)。我们来看看最常见的两种方式。**

****使用** `**filter()**`**

**`filter()`函数将**过滤出符合您的条件**的元素。在这个例子中，我们说“*过滤掉所有不等于苹果*的元素”。`filter()`创建一个新数组，而不是改变原来的数组。**

```
const fruits = ["apple", "pear", "banana"];const fruitsWithoutApples = fruits.filter(fruit => fruit !== "apple");console.log(fruitsWithoutApples);
// ["pear", "banana"]
```

> **`*filter()*` *遵循状态永不变异的函数式编程原则，可以在很多编程语言(Java、Python、Rust 等)中找到。)***

****使用** `**indexOf()**` **和** `**splice()**`**

**如果你同意改变状态(更新数组)，那么我们可以使用函数`indexOf()`和`splice()`的组合来删除一个特定的元素。**

**在本例中，让我们移除`"pear"`字符串。**

```
const fruits = ["apple", "pear", "banana"];const pearIndex = fruits.indexOf("pear"); // 1fruits.splice(pearIndex, 1); // second parameter represents how many elements to removeconsole.log(fruits);
// ["apple", "banana"];
```

# **检查数组是否包含特定元素**

**检查数组是否包含特定的元素是很有用的。让我们看看一些不同的选择。**

## **使用`indexOf()`**

**在这一点上，我们已经熟悉了`indexOf()`。如果你寻找的元素不在数组中，它将返回`-1`。**

```
const fruits = ["apple", "pear", "banana"];const orangeIndex = fruits.indexOf("orange"); // "orange" is not in array so -1 is returnedif (orangeIndex === -1) {
  // "orange" is not in array
} else {
  // "orange" is in array
}
```

## **使用`includes()`**

**更直接的方法是使用返回一个`Boolean`的`includes()`。**

```
const fruits = ["apple", "pear", "banana"];const isAppleInArray = fruits.includes("apple"); // true
```

# **检查变量是否是数组**

**在所有现代浏览器中，你可以使用`Array.isArray()`来确定一个变量是否是一个数组。**

```
const fruits = ["apple", "pear", "banana"];Array.isArray(fruits); // trueArray.isArray("orange"); // false
Array.isArray(99); // false
```

# **结论**

**JavaScript 中的数组类似于其他语言中的数组/列表/向量实现。当然，它有自己的怪癖和特点，其中一些值得注意。**

**在本文中，我们讨论了以下内容**

*   **什么是数组**
*   **如何创建数组**
*   **什么元素可以存储在数组中**
*   **基本数组操作以及如何执行这些操作**

***在*[*Twitter*](https://twitter.com/prplcode)*、*[*LinkedIn*](https://linkedin.com/in/simeg)*或* [*GitHub*](https://github.com/simeg) 上与我联系**

***最初发表于* [*prplcode.dev*](https://prplcode.dev/)**

***更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***