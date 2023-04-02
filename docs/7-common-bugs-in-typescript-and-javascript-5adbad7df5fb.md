# TypeScript(和 JavaScript)中的 7 个常见错误

> 原文：<https://javascript.plainenglish.io/7-common-bugs-in-typescript-and-javascript-5adbad7df5fb?source=collection_archive---------3----------------------->

## 以及如何修复它们。

![](img/17b7a007c1e0f876432ec6d4b1ec9350.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

是什么让你成为一名优秀的 TypeScript/JavaScript 开发人员？可能是因为你创造了一些很酷的项目，或者你在这个行业有多年的经验？不完全是。

您的代码应该总是正确运行。优秀的开发人员会使用 ESLint 这样的软件来确保他们使用最好的标准进行编码，并检查潜在的致命错误。外面有一个很好的软件叫 [SonarCloud](https://sonarcloud.io/) (没有任何隶属关系，我自己就用)。有了良好的配置，SonarCloud 和 ESLint 可以显著提高代码的质量，还能捕捉到您可能不知道的错误。

我明白了，不是每个人都研究 JavaScript 文档中的每一个小函数、API、类等等。但是知道一些你在编写代码时可能犯的无辜的错误是有好处的。

# 1)排序数组

*使用* `*Array.prototype.sort()*`时应提供比较功能

## 问题是

JS/TS 中的数组排序看起来非常简单；使用`Array.sort()`方法。但是有一个问题:试着运行下面的代码:

```
const arr = [1, 3, 20, 30];
arr.sort();
console.log(arr);
```

您可能希望 sort 方法按照升序对数字进行排序，将所有元素保持在相同的位置。相反，您会注意到元素按以下顺序排序:

```
[1, 20, 3, 30]
```

这显然没有正确排序。JavaScript 实际上将数字转换成字符串，然后按字母顺序对元素进行排序。JS 数组排序方法总是通过`string`进行排序。也就是说，只有在不提供比较函数的情况下。

## 解决方案

传入一个比较函数，并确保没有将值转换为字符串:

```
const array = /* some elements */
array.sort((a, b) => a - b);
```

# 2)与南京相比

`*NaN*` *不应用于比较*

## 问题是

在 JS/TS 中，有一种特殊的数字数据类型叫做`NaN`，它代表“不是一个数字”有时操作可能返回`NaN`而不是实际数字。这些操作中最常见的是`parseInt`和`parseFloat`。

让我们假设您正试图将一些用户提供的数据从一个`string`转换到`number`。由于它应该是一个整数，所以你选择使用`parseInt`，然后检查确保它的值是一个数字(不等于`NaN`)。您需要执行以下操作:

```
const value = parseInt(/* User data here */);if (value === NaN) {
    // Do stuff
}
```

这是不对的！即使使用`==`，与`NaN`比较的结果也总是假的。甚至`NaN`也不等于它本身。一般来说，你不应该使用总是以同样方式计算的条件句。

这个 bug 实际上给出了非常可预测的结果，但不是以你期望的方式，因为再一次，与`NaN`的比较总是错误的。

## 解决方案

ES2015 提供了对`Number.isNaN`的支持，因此您可以使用该功能来检查数字是否为`NaN`:

```
const value = parseInt(...);if (Number.isNaN(value)) {
    // Do stuff
}
```

如果你的目标是一个非常非常过时的浏览器，那么你应该使用这个符号:

```
const value = parseInt(...);if (value !== value) {
    // Do stuff
}
```

你可能首先认为`value`必须始终等于自身，所以这个永远不会计算到`true`。**那其实是错的**。由于`NaN`永远不能等于`NaN`，那么如果`value = NaN`那么`value !== value`将是`true`。

# Finally 块中的跳转语句

*跳转语句不应出现在*的“finally”块中

## 问题是

JS/TS 跳转语句有`return`、`throw`、`break`和`continue`。它们被称为跳转语句，因为它们使 JS 引擎跳转到代码中的另一点:

*   Return 语句跳出函数
*   Throw 跳出函数并引发错误
*   Break 跳出循环
*   继续跳转到循环的开始

在`finally`程序块中使用任何跳转语句都会导致意外行为:

```
function doSomething() {
    try {
        // Some code which might throw an error here
        return 1;
    } catch (err) {
        return 2;
    } finally {
        return 3;
    }
}
```

调用`doSomething()`时，如果在`try`块中没有抛出错误，您会期望返回`1`。如果抛出一个错误，那么你会期望返回`2`。相反，如果你调用`doSomething()`，你会注意到`3`是**总是**返回。这是因为如果提供了`finally`块，则**总是**运行。

## 解决方案

只需删除`finally`语句:

```
function doSomething() {
    try {
        return 1;
    } catch (err) {
        return 2;
    }
}
```

这确实是唯一的解决办法😐。

# 4)捕捉拒绝承诺

## 问题是

ES6 (ES2015)为 JavaScript 引入了大量令人惊叹的功能。有些人仍在学习诀窍。您可能已经在 NodeJS 中看到错误，未捕获的承诺拒绝将很快导致您的服务器退出，并返回非零退出代码。你自己可能也在浏览器中遇到过一些承诺拒绝错误；它们在控制台窗口中显示为 JavaScript 错误。

首先，处理这些错误的最简单的解决方案是用 try-catch 块包围承诺:

```
function doSomething() {
    try {
        axios.get(...).then(response => {
            // Do something
        });
    } catch (err) {
        // Handle the error
    }
}
```

使用常规的 try-catch 语句处理承诺拒绝是 JS/TS 中的一个常见错误。当试图在一个新的线程中完成一个操作时，比如发送一个网络请求，使用承诺。承诺有一种独立的方式来处理决心(承诺成功)和拒绝(承诺失败)。

## 解决方案(异步/等待)

这个问题最简单的解决方案是在包含承诺的函数中添加 async 修饰符，然后等待承诺:

```
async function doSomething() {
    try {
        const response = await axios.get(...);
        // Do some stuff with the HTTP response
    } catch (err) {
        // Handle the error
    }
}
```

用`async`定义一个函数/方法可以让 JavaScript 知道这个函数包含一个异步操作。关键字`await`告诉 JavaScript 停止当前线程，直到承诺解决。async/await 解决方案是用于 Promise 对象的 then/catch 链接方法的语法糖。

## 解决方案(然后/抓住)

处理承诺解析/拒绝的标准方式是对承诺对象使用`catch`函数:

```
function doSomething() {
    axios.get(...)
         .then(response => {
             // Do something
         })
         .catch(err => {
             // Handle error
         });
}
```

# 5)删除关键字

*删除关键字只应用于对象属性。*

## 问题是

在 JavaScript 中，声明一个变量有几个关键字:`var`(已经过时了)、`let`(在最里面的作用域声明)、和`const`(声明一个常量)。有时(这是不好的做法)，您可能会创建一个没有任何声明性关键字的变量:

```
myVariable = "hi";
```

尽管您不应该这样声明变量，但是您可以这样做。当你以这种方式声明一个变量时，你可以使用`delete`关键字来移除引用。这是因为`myVariable`实际上附加到了`window`对象上。如果你使用`var`、`let`或`const`声明一个变量，你不能使用 delete 关键字(你可以，只是它不起作用)。

关键字背后的主要意图是能够删除对象属性；例如，下面是你应该如何使用`delete`:

```
const data = { message: "Hello World", timestamp: Date.now() };delete data.message;
console.log(data); // data = { timestamp: ... }delete data.timestamp
console.log(data); // data = {}
```

## 解决方案

```
let myVariable: string | undefined = "Hello";// Use the variable heremyVariable = undefined
```

有时候你可能想“删除”一个变量。这通常是为了优化内存使用。在这种情况下，您应该将变量分配给`undefined`。这将释放与变量相关的内存。

在 TypeScript 中，您必须将变量赋给一个类型联合，将数据类型与`undefined`结合起来。

# 6)未过滤的 For-In 循环

*For-in 循环应始终过滤对象属性*

## 问题是

任何开发人员都会告诉你 for-each 循环可以节省大量时间。它们让你不用实例化那个`i`变量，并提供了一个简洁的语法框架。JavaScript 为迭代可迭代对象中的索引提供了良好的 for-in 语法。您可能见过类似这样的代码:

```
const array = [5, 6, 7, 8];
const obj = { name: "Bob", organization: "The Soggy Waffle" };for (let i in array) {
    console.log(array[i]);
}// orfor (let key in obj) {
    console.log(obj[key]);
}
```

不幸的是，这可能会导致错误。虽然 TypeScript 是面向对象的，但 JavaScript 不是。JavaScript 是基于原型的。有时候，在迭代数组或对象时，会遇到一些传递给对象的原型属性。特别是在 TypeScript 中，原型由 TSC 修改。

这可能会导致包含您不期望的键:

*   您不知道属性的存在，因为它是在原型链的更高层定义的
*   For-in 循环还可以通过

## 解决方案(针对阵列)

```
const array = [5, 6, 7, 8];array.forEach(n => {
    // Do stuff
});
```

与 for-in 语法不同，这类似于 for-each 循环。`n`是元素的值。如果您也需要索引，那么回调可以接受一个附加参数:

```
const array = [5, 6, 7, 8];array.forEach((n, i) => {
    // n is the value
    // i is the index
});
```

## 解决方案(针对对象)

数组附带了一组很好的函数，您可以将它们链接起来，但是普通的 JS 对象却不能。所以您可能需要使用 for-in 语法进行迭代。幸运的是，对象确实有一个名为`hasOwnProperty`的内置方法。这确保了您正在检查的属性在对象中正常存在。

```
const obj = /* Any object definition here */for (const key in obj) {
    if (obj.hasOwnProperty(key)) {
        // Do stuff here
    }
}
```

## 例外

这个规则有一个例外:当克隆一个对象时。

克隆 JS/TS 对象的基本代码是:

```
const obj = /* something */;
const newObj = {};for (const key in obj) {
    newOjb[key] = obj[key];
}
```

这不会引入错误，因为将一个对象的原型克隆到同一原型的另一个对象中不会产生任何意外的行为。

# 7)接口中的构造函数

*构造函数不应该在接口内部声明*

## 问题是

如果您使用没有任何类型定义的 JS 库，您可能已经创建了自己的`.d.ts`文件来指定类型，这样您就可以将代码包含在您的 TS 项目中。此外，您可能是 JS 代码的作者，并且希望提供类型声明，以便其他人可以在更广泛的项目中包含您的库。

对于一个类定义，您可能以前编写过这样的接口声明:

```
interface MyType {
    value: number;
    getValue(): number;

    constructor(value: number): MyType;
    // or
    new(value: number): MyType;
}
```

这实际上声明了一个名为`constructor`或`new`的方法，并且实际上会在将来引入更多的类型脚本错误。

## 解决方案

相反，您应该提供一个类声明:

```
declare class MyType {
    value: number;
    getValue(): number; constructor(value: number);
}
```

我希望这篇文章对你有所帮助。如果你学到了一些你还不知道的东西，并且想通过解决这些鲜为人知的错误来改进你的代码，这里是我的建议:

*   关注一个关于 JavaScript 的媒体出版物*(用简单英语写的 JavaScript 是一个很好的例子)*
*   通过林挺软件运行你的代码*(ESLint，Codacy，SonarCloud 都是不错的选择)*
*   永远不要停止学习！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*