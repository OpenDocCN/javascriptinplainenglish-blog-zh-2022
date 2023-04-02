# JavaScript Spread 和 Rest 操作符:何时使用它们

> 原文：<https://javascript.plainenglish.io/javascript-spread-and-rest-operators-when-to-use-them-1d20f43f4a87?source=collection_archive---------5----------------------->

## 何时以及如何使用 JavaScript Spread 和 Rest 操作符。

![](img/b3db3b576fc9cf8c3bb65b1873c5494b.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我花了很长时间才听说 spread 和 rest 操作符。作为三个句号字符，`...`spread 和 rest 运算符在使用时看起来相同，但它们的用法却大不相同。从某种意义上说，它们是对立的。

**当一个数组的所有元素都需要“展开”到一个列表中时，使用 spread 运算符。**

**rest 操作符用于收集多个元素，并将它们压缩成一个数组。**

让我们深入了解如何使用它们。

# 传播算子

扩展运算符可用于在需要传递多个参数的地方扩展数组，如函数或另一个数组。其用途可能是以下任何一种:

## 传递给函数

给定一个函数`function doStuff(x, y, z) { }`，我们通常会用三个独立的变量或值来调用它，比如`doStuff(1, 2, myVar)`。

让我们假设我们有一个数组`let myVals = [1, 2, 3]`。通过使用 spread 操作符:`doStuff(...myVals)`，我们可以将数组中的每个元素作为单独的参数传递给上面的函数。

我们甚至可以多次使用 spread 操作符。给定一个函数`function doComplicatedStuff(a, b, c, d, e, f) {}`，使用 spread 操作符，我们可以像这样调用它:

```
let myVars = [2, 3];
doComplicatedStuff(1, ...myVars, ...myVars, 6);
```

在上面的例子中，`myVars`被传递给参数 b 和 c，然后再次被传递给参数 d 和 e。

对于对象构造函数，我们可以类似地使用 spread 运算符:

```
let dateFields = [1970, 0, 1];  // 1 Jan 1970
let d = new Date(...dateFields);
```

## 复制和连接数组

在学习 spread 操作符之前，我将使用`slice()`函数复制数组，该函数对给定数组的一部分执行浅层复制。使用 spread，我们可以执行数组的浅层复制，如下所示:

```
let arr = ["milk", "eggs", "cheese"];
let clonedArr = [...arr];
// clonedArr is now a copy of arr
```

现有数组也可以“注入”到新的数组文字中:

```
let arr = ["milk", "eggs", "cheese"];
let newArr = ["ham", ...arr, "butter"];
```

它们也可以连接在一起:

```
let list1 = ["milk", "eggs", "cheese"];
let list2 = ["ham", "butter"];
let combinedList = [...list1, ...list2];
// combinedList now equals ["milk", "eggs", "cheese", "ham", "butter"]
```

**警告:
因此，它不应该用于多维数组。**

## 复制和修改对象文字

与 spread 运算符在数组上的使用方式类似，它们也可以在对象的可枚举属性上使用。要克隆对象:

```
let obj1 = {a: "thing", b: 39};
let obj2 = {...obj1};
// obj2 = obj1
```

要合并对象:

```
let obj1 = {a: "thing", b: 39};
let obj2 = {c: "second thing", d: 60};
let mergedObj = {...obj1, ...obj2};
```

但是，请注意，合并对象集合中最后一个要合并的对象优先于共享属性。也就是说，共享属性`a`的两个对象的值`a`将等于两个合并对象中的第二个。就像:

```
let obj1 = {a: "thing", b: 39};
let obj2 = {a: "second thing", d: 60};
let mergedObj = {...obj1, ...obj2};
// mergedObj now equals {a: "second thing", b: 39, d: 60}
```

# Rest 运算符

一旦我们理解了 spread 操作符，我们可以看到 rest 操作符有点像相反的情况。然而，与 spread 操作符不同，rest 操作符只用于一个目的:**给函数一个不确定或可变数量的输入参数**。

考虑以下函数及其调用:

```
function doThings(a,  b, ...others) { 
   console.log(others);
}

doThings("one", "two", "three", "four", "five", "six");
// Output: "['three', 'four', 'five', 'six']"
```

`doThings`函数可以用我们想要的两个或多个参数来调用。第一个传递的参数将被赋给`a`，第二个被赋给`b`，其他的都将被组合成一个数组。如果没有传递额外的参数，那么`others`将是一个空数组。

重要的是要知道 rest 操作符在函数定义中只能使用一次，而且只能用于最后一个参数。因此，以下两个例子都是**不正确的:**

```
function doThings(...a, b, ...c) { // stuff }
// **Incorrect because it has two rest parameters** function doThings(a, ...b, c) { // stuff }
// **Incorrect because the rest parameter is not the last parameter**
```

注意，rest 参数和`[arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)`对象不是一回事。`arguments`对象不是真正的数组，而其余的参数是。此外，`arguments`对象包含传递给函数的所有**参数，而 rest 参数只包含传递给 rest 参数本身的参数。**

既然我已经研究了这两个多才多艺的操作符，我已经开始在我的项目中使用它们，我希望你也能这样做。

## 额外阅读:

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) [## Rest 参数- JavaScript | MDN

### rest 参数语法允许函数接受不确定数量的参数作为数组，提供了一种方法…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) [## 扩展语法(...)- JavaScript | MDN

### 扩展语法(...)允许诸如数组表达式或字符串的可迭代对象在零或…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) 

*更多内容请看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***