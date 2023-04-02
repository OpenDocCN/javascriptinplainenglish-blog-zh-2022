# 你认为你知道 var，let 和 const 的区别吗？

> 原文：<https://javascript.plainenglish.io/you-think-you-know-the-difference-between-var-let-and-const-b55b638529fc?source=collection_archive---------3----------------------->

## 来分享你的想法。

![](img/4ccb8e610791d1469b8f6e47f4617bf6.png)

Photo By [**Oskar Yildiz**](https://www.instagram.com/oskaryil/)

嘿朋友们，

很久以前我讲过[**JavaScript 提升影响你代码的 3 种方式**](/3-ways-javascript-hoisting-affects-your-code-a6a93626c600) **。**剧透警告:提升对用`var`、`let`和`const` 声明的变量有不同的影响。如果您想了解更多，请查看这篇文章。

在本文中，我想通过区分这三个关键词来进一步展开讨论。具体来说，我想回答以下几个问题:**有什么区别？什么时候应该使用它们？**

最近，我在一个专业场合被问到这两个问题。虽然我提供了一个充分的答案，但我更愿意提供一个特别的、有见地的答案。既然我错过了机会，我现在就要帮你提供一个华丽的答案，当将来有人问你的时候。我保证你会是这个街区最聪明的人。

让我们开始吧。

# 关键词:常量

真正的讨论更多的是关于`let`和`var`的，所以让我们快速解决`const`的问题。

`const`用于**运行时**值不变的变量。一个非常流行的例子是圆周率的值。

如果我们想创建一个存储 pi 值的变量`pi`，我们可以将它存储在一个 const 中。为什么？因为我们永远不会更新圆周率的值。

这里有一个例子:

```
function findPerimeterCircle(radius){
    const pi = 3.14159265359;
    return 2 * pi * radius;
}console.log(findPerimeterCircle(5))
```

再举个例子？

假设我们正在创建一个棋盘。标准棋盘有 64 个方块。它们是 8x8 的。

```
const numRows = 8;
const numCols = 8;
```

在运行时，我们不会神奇地改变行数或列数。如果你真的想，在未来的更新中，你可以让董事会更大。然而，在运行时，这些值永远不会改变。

那真的很重要。

**const 的另一个真正重要的属性是它有一个块级范围。**

```
function findPerimeterCircle(radius){
    const pi = 3.14159265359;
    return 2 * pi * radius;
   ** console.log(pi) //3.14159265359**
}**console.log(pi) //not defined**if(true){
    const x = 4;
    **console.log(x); //4**
}
**console.log(x); //not defined**
```

在 Javascript 中，我们有全局作用域、函数作用域和块作用域。全局范围基本上意味着一个变量在任何地方都是可访问的。函数作用域意味着变量只能在函数内部访问。块级作用域意味着变量包含在最近的一组花括号中。

在上面的示例代码中，我们看到 pi 存在于函数中。功能之外，不存在。如果你尝试打印到控制台，它会说“pi 未定义”。这是有道理的。如果你有 Javascript 的经验，你会知道`let`、`var`和`const` 都是这样反应的。

但是让我们看看接下来的几行，这是一个 if 语句。

变量 x 包含在一组花括号中。而且由于是一个`const`变量，变量 x 不存在于花括号之外。

```
if(true){
    var x = 4;
    **console.log(x); //4**
}
**console.log(x); //4**
```

如果我们用 var 代替 const，那么它实际上是可行的。如上图所示。因为我们使用的是 const，所以它不起作用。

这也称为块级范围。同样，常量变量只存在于最接近的花括号中。

这是概要。如果你需要存储一个永远不会改变值的变量，并且有一个块级的作用域，const 是你的好朋友。大多数情况下，您可能不会使用 const。

# 关键词:让

希望你注意到了前面的部分。与`const`类似，用`let` 声明的变量有一个块级范围。那是什么意思？跟我重复一遍:变量只存在于最接近的一组花括号中。

与`const`不同，用`let` 声明的变量值可以在运行时改变。

```
let x = 2;
x= 5;
x= 200;
```

这完全合法。如果您有 Java 或 C 之类的其他语言的经验，您可能也会喜欢 Javascript 中类型转换的惊人之处。

```
let x = 2; //number 
x = false; //boolean
x = "Kyle DeGuzman" //string
```

上面的示例代码也是完全合法的！这是惊人的东西。

但是，使用`let` 关键字，您不能“重新声明”变量。

```
let x = 5;
let x = 400;  //ERROR
let x = "Kyle needs a French Bulldog"; //ERROR
```

这是不允许的。它会告诉你 x 已经存在。这是`let`和`var`的主要区别。

如果我们用`var`代替`let`，你会得到如下结果:

```
var x = 5;
var x = 400;
var x = "Kyle needs a French Bulldog";
```

…这很好。这会有用的。这将只是更新 x 的值。

以上是`let`的概要。同样，`let`有一个块级范围。您可以在运行后更改该值，但不能重新声明同一个变量。在提升方面也有不同，但是你可以在其他地方读到。

# 关键词:var

```
var x = 5;
var x = 400;
var x = "Kyle needs a French Bulldog";
```

我们知道这很好。

您现在可能知道，与`let` 和`const`不同，`var` 没有块级范围。

```
if (true){
   var x = 4;
}
console.log(x); //4
```

这是可行的。4 将被打印到控制台。如果那是`let` 或`const`，那就不行。它会说 x 是未定义的。

与`let` 和`const`不同，`var`有一个函数级的作用域。同样，这意味着变量存在于函数的任何地方。

```
function add(){
    var x  = 5;
    console.log(x); //5
}
```

以上，直截了当。5 将被打印到控制台。

```
function add1(){
    console.log(x); //undefined
    var x  = 5; 
}
function add2(){
    console.log(x); //ERROR: x is not defined
    let x  = 5; 
}
```

这个呢？在给`x`赋值之前，看看我们是如何将`x`打印到控制台的。

如果我们使用`var`，变量 x 将在函数中处处存在**。这也意味着变量在声明或初始化之前就已经存在了！所以当 add1()说‘undefined’时，这意味着“是的，变量存在，但是它还没有赋值”。**

相比之下，使用`let`变量，变量 x 将在声明或初始化之后开始存在。因此，当 add2()呈现错误时，这意味着“变量不存在。我们不知道你在说什么。”

这里是要点:如果您需要函数级作用域，var 是很好的选择。如果你想一遍又一遍地重新声明变量，var 是很棒的。

但是，您真的需要 var 来做到这一点吗？

# let vs var

如果你真的需要一个函数级的作用域，那么在函数的顶部声明一个`let`变量。

```
function add(){
    let x=5; 
    console.log(x)
}
```

现在你有了一个函数级变量。

不要一遍又一遍地声明同一个变量，而是选择一个新的变量名或更新变量值。

```
let x = 5;
let x = 6; //ERROR
let x = 7; //ERROR
```

首先，没有其他语言允许这样做。

没有其他语言允许你在声明变量之前使用它们。可以说，如果在声明变量之前就使用它们，看起来很糟糕。这肯定会影响代码的可读性，尤其是当别人要查看它的时候。

如果你看，很多人远离`var`。人们认为`var`是杂乱和不必要的。随着 ES6 和 let 关键字的引入，很多人会告诉新人只需坚持`let`。在很大程度上，我同意。

为了这篇文章，我看了许多不同的意见和论点。普遍的共识是没有人应该使用`var`。几乎没有什么情况下，你应该使用`var` 而不是`let`。

我会说，有一个论点我可以提供一盎司的支持。一定要读一读。

[](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/apA.md#var-and-let) [## 第二版 getify/You-don-Know-JS/APA . MD

### 现在，我们将围绕本书正文中涵盖的许多主题探讨一些细微差别和边缘。这个…

github.com](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/apA.md#var-and-let) 

在这个 md 文件中，作者为`var`做了一个公平的案例。他们的论点是语义学。我真的鼓励你阅读部分 **var 和 let。**很有启发。

其中一句关键的名言是:

> 如果你在任何地方都使用`let`，那么哪些声明被设计成本地化的，哪些声明打算在整个函数中使用就不那么明显了。

所以，再一次，这个想法是通过有策略地选择你使用的关键字来为你的代码提供语义。

我喜欢这样。

但是我的问题是:如果普遍的共识或者流行的观点是`var` 是无用的，大多数开发者可能不会理解你选择使用`var` 和`let`背后的语义。他们可能不会再考虑你两个都用的事实。

因此，虽然我认为它很聪明，但我不认为它会有效。如果你选择赋予它那个语义，只有你会知道它。其他人都不知道这件事。

但当然，我的观点是建立在大多数人认为`var` 没用的前提下。你同意前提为真吗？你个人对什么时候用`var`和`let`有偏好吗？

如果面试官问你什么时候会使用其中一个，你会怎么回答？我真的很好奇。

这就是我对`const`、`var`和`let`的看法。

我对别人说的话非常感兴趣。

感谢阅读。

*更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***