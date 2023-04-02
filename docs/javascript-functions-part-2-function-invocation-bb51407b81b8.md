# 通过精确的函数调用展现您的 JavaScript 开发能力

> 原文：<https://javascript.plainenglish.io/javascript-functions-part-2-function-invocation-bb51407b81b8?source=collection_archive---------20----------------------->

## JavaScript 函数第 2 部分:函数隐式参数和调用函数

![](img/f202e75b8164241bc385914135720535.png)

*这是第一篇文章的延续:*

[](/javascript-functions-part-1-definitions-and-arguments-ef2643e73233) [## 作为一名 JavaScript 开发人员，3 个函数概念将成为你的武器库

### JavaScript 函数第 1 部分:函数定义和参数赋值

javascript.plainenglish.io](/javascript-functions-part-1-definitions-and-arguments-ef2643e73233) 

在这篇博客中，我们将讨论以下主题:

*   函数隐式参数
*   以各种方式调用函数

## 1.函数隐式参数:`“arguments”`和" this "

从[第 1 部分](https://medium.com/@shriomtripathi33/javascript-functions-part-1-definitions-and-arguments-ef2643e73233)我们了解了函数*参数*(作为函数定义的一部分列出的变量)和函数*参数*(调用函数时传递给函数的值)之间的区别。)*。所以当我们调用一个函数时，有两个参数被隐式地传递给函数，`arguments`和`this`。*

这些参数没有在函数签名中显式指定，因此它们被认为是隐式的。

**1.1** `**arguments**` **参数**

提供给函数的所有参数都收集在`arguments`参数中。它用于访问函数的所有参数。它允许我们使用函数重载，这是 JavaScript 本身不支持的。
自从在 ES6 中引入`rest`参数后，`arguments`参数的使用显著减少。让我们看看实现参数是如何工作的。

`arguments`对象有一个合适的*长度*来表示参数的数量。单个参数值可以通过使用数组//索引符号获得；例如*论据【6】。*

```
Sample 1 :
// [https://www.w3schools.com/js/js_function_parameters.asp](https://www.w3schools.com/js/js_function_parameters.asp)x = findMax(1, 123, 500, 115, 44, 88);
function findMax() {
   let max = -Infinity;
     for (let i = 0; i < arguments.length; i++) {
       if (arguments[i] > max) {
       max = arguments[i];
       }
     }
     return max;
 }console.log(x)// output
500Sample 2 :
function nowhere(a, b, c) {
    console.log(a, b, c);
    console.log(arguments)
}// output
nowhere(3,4,5,6)
3 4 5
[Arguments] { '0': 3, '1': 4, '2': 5, '3': 6 } 
```

严格模式:

严格模式是对 JavaScript 的 ES5 增强，它导致错误被抛出，而不是被 JavaScript 引擎安静地拾取。一些语言特性的行为已经被改变，一些潜在有害的语言特性已经被彻底禁止(稍后将详细介绍)。严格模式禁用参数别名，这是它的改进之一。

将函数参数与 arguments 对象混为一谈可能会令人困惑。让我们看看下面给出的例子，以避免混淆。

```
"use strict"function handleBomb(country) {
 console.log(arguments)
 arguments[0] = 'Japan';
 console.log(country, arguments[0])
}handleBomb('USA')
// output
[Arguments] { '0': 'USA' }
USA Japan
```

为了更好地理解，请参考这篇文章:

[](http://qnimate.com/javascript-strict-mode-in-nutshell/) [## 带示例的 Javascript“使用严格”教程

### 编辑描述

qnimate.com](http://qnimate.com/javascript-strict-mode-in-nutshell/) 

**1.2** `**this**` **参数**

`this`参数是面向对象 JavaScript 的一个重要组成部分，指的是与函数调用相关联的对象。因此，它被称为功能*上下文。*

函数上下文是来自面向对象语言如 Java 的一个概念。他们可能认为他们理解了`this`，因为在这种语言中`this`指向定义了该方法的类的一个实例。

但是我们将在下面的上下文中看到，JavaScript 中的`this`依赖于函数调用的方式。因为理解`this`参数的确切性质是面向对象 JavaScript 最重要的支柱之一。

## 2.以各种方式调用函数

**2.1 作为函数调用**

别被标题搞糊涂了，调用“*作为函数*”是为了和其他调用机制区分开来:*方法*、*构造函数*和`apply` */* `call` *。*

当使用`()` 操作符调用函数，并且应用了`()`操作符的表达式没有将函数作为对象的属性引用时，就会发生这种类型的调用。

```
// function declaration invoked as a function
function hero() {};
hero()// function expression invoked as a function
var superman = function () {};
superman();// Immediately invoked function expression, invoked as function
(function(){})()
```

当我们以这种方式调用函数时，函数的上下文(`this`关键字)可以是两个东西:在非严格模式下，它将是全局上下文(窗口对象)，在严格模式下，它将是未定义的。

**2.2 作为方法调用**

当一个函数被赋予一个对象的属性，并且通过引用该属性来调用该函数时，该函数被称为该对象的方法。

```
const hero = {}
hero.superman = function(){};
hero.superman()
```

这里先来了解一下*法*这个词。来自面向对象的背景，您会记得方法所属的对象在方法体中是可用的，如`this`。同样的事情也发生在这里。当一个函数作为一个对象的方法被调用时，该对象成为函数上下文，并通过`this`参数在函数中可用。这意味着 JavaScript 允许编写面向对象的代码。

```
function provideContext() {
 this.exceptionHero = 'Vision'
 return this;
}const contextHandler = {
 orgName: 'Marvel',
 provideSuperHeroContext: provideContext
}console.log('---1---')
console.log(provideContext())console.log('---2---')
console.log(contextHandler.provideSuperHeroContext())// output
---1---
Object [global] {
  global: [Circular],
  clearInterval: [Function: clearInterval],
  clearTimeout: [Function: clearTimeout],
  setInterval: [Function: setInterval],
  setTimeout: [Function: setTimeout] {
    [Symbol(nodejs.util.promisify.custom)]: [Function]
  },
  queueMicrotask: [Function: queueMicrotask],
  clearImmediate: [Function: clearImmediate],
  setImmediate: [Function: setImmediate] {
    [Symbol(nodejs.util.promisify.custom)]: [Function]
  },
  exceptionHero: 'Vision'
}
---2---
{
  orgName: 'Marvel',
  provideSuperHeroContext: [Function: provideContext],
  exceptionHero: 'Vision'
}
```

**注意:**为了以面向对象的方式编写 JavaScript，函数必须作为方法被调用。这允许您在任何方法中使用`this`来引用方法的**所有者**对象，这是面向对象编程中的一个基本思想。

**2.3 作为构造函数调用**

构造函数的声明就像其他函数一样，我们可以使用函数声明或函数表达式来构造新的对象。只有数组函数有点不同。主要的区别总是来自于函数调用的方式。

为了将函数作为构造函数调用，我们在函数调用之前添加了关键字`new`。

```
function Marvel() {}const marvel = new Marvel()
```

**2.3.1 构造函数是函数的类固醇**

让我们来看看:

```
function HeroOrg() {
 this.groundRules = function() {
  return this;
 }
}const marvel = new HeroOrg()
const dc = new HeroOrg()console.log('---1---')
console.log(marvel.groundRules() === dc.groundRules())console.log('---2---')
console.log(marvel.groundRules() === marvel)//output
---1---
false
---2---
true
```

我们创建一个名为 *HeroOrg* 的函数，它将用于构造。我们创建两个实例*惊奇*和 *dc* 。构造函数在这个对象上创建了一个名为 *groundRules* 的属性，这个属性被赋予了一个函数，使得这个函数成为新创建的对象的一个方法。

构造函数调用时会发生一些事情:

*   创建一个新的空对象。
*   这个创建的对象作为`this`参数传递给构造函数，并因此成为构造函数的函数上下文。
*   构造函数对象作为`new`操作符的值返回。

构造函数的工作是构建一个新对象，配置它，并将其作为构造函数的值返回。任何阻碍这一目标的事情对构造者来说都不是好事。

**2.3.2 构造函数返回的值**

```
function Hero() {
 this.name = 'Superman'
 return 'sucess'
}const hero1 = new Hero()
const hero2 = Hero()console.log('---1---')
console.log(hero1)console.log('---2---')
console.log(hero2)//output
---1---
Hero { name: 'Superman' }
---2---
sucess
```

从上面的例子可以看出，当一个函数作为构造函数被调用时，构造函数创建的新对象被返回。如果我们调用一个没有`new`关键字的函数，那么最终的返回语句值将被返回或`undefined`。

**2.4 使用** `**apply**` **、** `**call**` **和** `**bind**` **方法**

到目前为止，我们已经看到`this`是函数、全局或对象上下文的前缀，这取决于调用。JavaScript 还允许我们将函数的上下文设置为自定义对象，即覆盖`this`。我们可以使用每个函数都有的两种方法来实现这一点:`apply`和`call`。

**2.4.1 应用**

为了通过`apply`方法调用一个函数，我们向`apply`传递两个参数，一个是作为函数上下文的对象，另一个是一组值。

如需更多详细信息，请查看:

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) [## function . prototype . apply()-JavaScript | MDN

### 该方法使用给定的 this 值和作为数组(或类似数组的对象)提供的参数调用函数。的…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 

```
function fly() {
 console.log(this.org)
 console.log(...arguments)
}const customPower = { org: 'marvel'}
fly.**apply**(customPower, ['thor', 'ironman', 'vision'])// output
marvel
thor ironman vision
```

因为我们可以设置我们已经通过`apply`传递了 *customPower* 作为 fly 函数的上下文。如果是普通的调用，`this`应该指向全局对象作为上下文，但是我们用自定义对象作为上下文覆盖了它。

```
const heroOrg = {
 fly: function () {
  console.log(this.org)
  console.log(...arguments)
 }
}const customPower = { org: 'marvel'}
heroOrg.fly.**apply**(customPower, ['thor', 'ironman', 'vision'])//output
marvel
thor ironman vision 
```

**2.4.2 调用**

call 方法也以类似的方式使用。我们传递的不是参数数组，而是参数列表。

```
function fly() {
 console.log(this.org)
 console.log(...arguments)
}const customPower = { org: 'marvel'}
fly.**call**(customPower, 'thor', 'ironman', 'vision')//output
marvel
thor ironman visionconst heroOrg = {
 fly: function () {
  console.log(this.org)
  console.log(...arguments)
 }
}const customPower = { org: 'marvel'}
heroOrg.fly.**call**(customPower, 'thor', 'ironman', 'vision')//output
marvel
thor ironman vision
```

**2.4.3 绑定**

`bind`方法可用于所有函数，其设计目的是*创建*并返回一个绑定到传入对象的*新*函数。

```
const marvel = { name: "Marvel", leader: 'Nick Fury' }
const dc = { name: "DC", leader: 'Batman'}function printOrgnizationDetail() {
 console.log(`Name: ${this.name}, Lead: ${this.leader}`)
}const marvelOrg = printOrgnizationDetail.**bind**(marvel)
const dcOrg = printOrgnizationDetail.**bind**(dc)marvelOrg()
dcOrg()//output
Name: Marvel, Lead: Nick Fury
Name: DC, Lead: Batman
```

**注意**:箭头函数(lambda 函数)有限制。“**调用**”、“**绑定**、“**应用**”不能用于数组函数。为了更好地理解箭头功能，请查看以下内容:

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) [## 箭头函数表达式- JavaScript | MDN

### arrow 函数表达式是传统函数表达式的一种紧凑替代形式，但它是有限的，不能…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 

这就是 JavaScript 函数的全部进展。我希望你已经发现这是有用的。感谢您的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*