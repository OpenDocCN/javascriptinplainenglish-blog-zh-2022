# 理解 JavaScript 中的作用域

> 原文：<https://javascript.plainenglish.io/understand-scoping-in-javascript-299e88b2989b?source=collection_archive---------7----------------------->

## 理解 JavaScript 中的一个重要主题——作用域。

![](img/40d223aed6ab446dde96d9d0aa6d75df.png)

Photo by [Luca Bravo](https://unsplash.com/@lucabravo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> 要理解 JavaScript 中的作用域是什么，首先必须理解一个叫做提升的重要概念。我将在这里简单地讨论变量提升，而不是函数提升，但是我建议在这里更好地了解这个概念。

# 什么是吊装？

提升是指在代码执行之前，解释器将变量、函数和类声明移动到其各自*范围顶部的过程。*只提升声明，不提升它们的初始化。**

这有助于我们在声明变量、函数和类之前使用它们，但这不是好的做法，因为它可能会导致错误。

让我们看看变量的提升是如何工作的:

## →提升带有“var”关键字的变量

```
var a = "hello";
console.log(a); // prints "hello". 
```

提升期间:

```
var a; // Declaration
a = "hello"; // Initalization
console.log(a); // prints "hello".
```

如果我们试图访问一个使用`var`声明的变量，在它被初始化之前，我们会得到*未定义的*，因为带有`var`的变量的默认初始化是*未定义的*。

```
console.log(a); // prints undefined.
var a = "hello"; // Initalization
```

## →使用“let”和“const”关键字提升变量

使用`let`或`const`定义的变量的提升与使用`var`定义的变量相同。带有`let`或`const`的变量与使用`var`定义的变量之间的唯一区别在于默认的初始化值。

当我们在`var`变量初始化之前访问它时，我们得到了未定义的变量，因为这是`var`变量的默认初始化。但是在`let`或`const`变量的情况下，不存在默认初始化。

如果我们试图访问`let`或`const`变量，我们会得到一个引用错误，说明我们试图在变量初始化之前访问它。请参见下面的示例:

```
console.log(a); // ReferenceError: Cannot access 'a' before initialization"
const a = 'hello';
```

# 辖域

JavaScript 中的范围是指与当前执行上下文相关的变量的可访问性。JavaScript 中有 3 种作用域:I)全局作用域，II)函数作用域，III)块级作用域。

JavaScript 中的作用域取决于*如何定义变量*，即使用`var`、`let`或`const`关键字。它还取决于变量在哪里定义的*，即在全局执行上下文中，还是在函数或块中(if-else，for 循环，等等)。*

现在，让我们看看*如何以及在哪里定义*一个变量会影响它的可访问性。

# 变量的可访问性

全局执行上下文指的是没有在任何函数、任何块或任何类中定义的代码，你懂的。在全局执行上下文中定义的变量可以在代码中的任何地方使用。

使用`var`定义的变量只支持全局和功能级作用域，不支持块级作用域。而`let`或`const`变量支持所有三个。

看看下面的例子:

```
var globalVariable = 'hello world'; // variable in the global execution scopefuntion test() {
  console.log(globalVariable);
}
test(); // 'hello world'
```

这里，变量“globalVariable”被定义在函数外部的全局作用域中，所以我们可以在“test”函数中访问它。

考虑下面的另一个示例，并尝试猜测以下内容的输出:

```
var a = 'hello';function test() {
  var a = 'hey';
  console.log(a);
}
test();
console.log(a);
```

这里，函数 test 内的第一个“console . log”*将打印“hey”，函数*外的第二个“console . log”*将打印“hello”。变量“a”在全局执行上下文中，具有全局范围，但是函数“test”中的变量“a”具有函数范围，因为该变量是在函数本身内部定义的。*

因此，当上面的代码运行时，由于提升会发生以下情况:

```
var a; // variable "a" is declared
a = 'hello'; // variable "a" is initializedfunction test() {
  var a;  // variable "a" is moved to the top of its scope
  a = 'hey'; // now the functional scope variable "a" is intialized
  console.log(a); // "hey"
}
test();
console.log(a); // "hello"
```

现在，假设这是代码:

```
var a= 'hello';function test() {
  a = 'hey';
  console.log(a); // "hey"
}
test();
console.log(a); "hey"
```

这里，由于在函数内部，我们没有使用`var`、`let`或`const`关键字来定义变量，它自动在全局范围内引用变量，并将其值从“hello”更新为“hey”。这就是为什么我们在控制台中看到“嘿”打印两次。

看看另一个例子:

```
var a = 'hello';if(true) {
  var a = 'hey';
  console.log(a);
}console.log(a); 
```

你能猜出上面代码的输出吗？。如果你对两个“console.log”的回答都是“嘿”,那么你就对了。我们第二次看到“嘿”而不是“你好”的原因是因为`var`关键字。由于使用`var`定义的变量范围仅限于全局和函数范围，它们不适用于块级范围。在这种情况下，发生提升时，代码如下所示:

```
var a; 
a = 'hello';if(true) {
  a = 'hey';
  console.log(a);
}console.log(a);
```

因为“var”关键字不支持块级作用域，所以它引用了全局作用域中的变量“a”。

所以，在 JavaScript 的 **ES6(2015)** 之前，只有一种方法可以使用`var`关键字声明变量。ES6(2015)引入了`let`和`const`——声明变量的新方法。`let`和`const`为 JavaScript 中的变量启用了块级范围。

让我们看看前面的例子，但是我们将使用`let`而不是`var`来声明一个变量。

```
let a = 'hello';if(true) {
  let a = 'hey';
  console.log(a); // prints "hey"
}console.log(a); // prints "hello"
```

这里第一个 *console.log* 印“嘿”，第二个印“你好”。这是因为`let`关键字及其提供的块级范围。如果我们使用关键字`const`而不是`let`，同样的事情也会发生。让我们在吊装时看看上面的代码:

```
let a;
a = 'hello';if(true) {
  let a;
  a = 'hey';
  console.log(a); // prints "hey"
}console.log(a); // prints "hello"
```

使用`let`声明的变量值可以更新，但是使用`const`声明的变量值不能更新。

当使用`let`或`const`声明一个变量时，我们不能在这个特定的作用域中用相同的名字命名另一个变量，但是可以在另一个作用域中重复这个名字。

看看另一个例子:

```
var a = 'hello';function scope() {
  if(a !== undefined) {
   var a = 'hey';
  }
  console.log(a);
}scope();
```

在这里,“console.log”将打印“undefined”而不是“hey ”,因为我们知道`var`变量不支持块级作用域，只支持全局和函数级作用域。这是在吊装过程中发生的:

```
// GLOBAL SCOPE
var a;
a = 'hello';function scope() {
 // FUNCTIONAL LEVEL SCOPE 
  var a;
  if(a !== undefined) { // this conditional evaluated to false since "a" is undefined (as seen in hoisting)
   a = 'hey';
  }
  console.log(a); // this "a" refrenced the variable "a" in the functional level scope and the not the variable "a" in global scope.
}scope();
```

让我们使用`let`或`const`更新上面的代码，

```
let a = 'hello';function scope() {
  if(a !== undefined) {
   let a = 'hey';
    console.log(a); // prints "hey".
  }
  console.log(a); // prints "hello".
}scope();
```

这里," if "块中的第一个" console.log "打印" hey ",第二个" console.log "打印" hello"。让我们看一下吊装，以便更好地理解:

```
let a;
a = 'hello';function scope() {
  if(a !== undefined) {
    let a;    
    a = 'hey';
    console.log(a); // prints "hey".
  }
  console.log(a); // prints "hello".
}scope();
```

这里,“if”*条件*中的变量“a”引用了全局作用域中的变量“a ”,因为函数级作用域中没有变量“a”。

在“if”条件中，我们创建了一个新变量“a ”,由于它是使用`let`定义的，提升过程只将这个变量移动到块级范围的顶部，而没有移动到函数级范围的顶部，因为`let`和`const`支持块级范围。

因此，第一个“console.log”引用了“if”块级范围内的变量，第二个“console.log”引用了全局范围内的变量，因为在功能级范围内没有变量“a”。

# **结论:**

希望现在变量提升和变量作用域的概念对你来说更清楚了。这些是 JavaScript 中最重要的概念，每个 JavaScript 开发人员都必须理解。这些主题不仅在为你的应用程序编写代码时会派上用场，在面试时也会派上用场。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*