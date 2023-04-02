# JavaScript 中的箭头函数:Javascript 面试问题(ES 6)

> 原文：<https://javascript.plainenglish.io/javascript-interview-questions-arrow-functions-9fd21bb1d48c?source=collection_archive---------6----------------------->

## JavaScript 面试问题# 2:什么是箭头函数，普通函数&箭头函数有什么区别？

![](img/caae80eec8ae09c10dc2878e2bd3eaa6.png)

# JavaScript 面试问题# 2

什么是箭头函数，普通函数和箭头函数有什么区别？

大家好，今天我们将了解什么是箭头函数，并且我们将通过例子回答 JavaScript 访谈中最常见的问题之一。

让我们从正则函数的外观开始。

## 常规函数

```
// Regular function expression
function multiply(x,y){
  return x * y;
}multiply(3,5) // Call the function15
```

如你所见，我们将函数定义为`multiply`，并将参数传递为 **x** 和 **y** ，并返回 **x * y**

让我们看看如何在箭头函数中编写这个函数

## 箭头功能

```
// Declaring the multiply function with arrow function
const multiply = (x,y) => x*ymultiply(3,5) // Call the function15
```

正如你所看到的，我们已经减少了我们编写的代码行数，并且完全降低了 arrow 函数的复杂性。这是使用箭头函数的好处之一。

让我们仔细看看我们的**箭头函数语法:**

```
const functionName = (argument1, argument2, ...argumentN) => {
  return (
    // write your statements here with parameters
    argument1 * argument2 // as our first example
  )
}
```

正如你在这里看到的，**函数名**是箭头函数的名称。

**argument 1**、 **argument2 和 argumentN** 是我们可以在 arrow 函数中使用的参数。我们可以根据需要添加任意多的参数。这和我们对常规函数做的事情是一样的。

return (…) 之间的最后一件事是定义我们的函数体。

如果我们的函数体中只有一条语句，我们也可以简化 arrow 函数，如下所示:

```
const functionName = (argument1,argument2) => argument1 * argument2}
```

**示例 1:不带参数的箭头函数**

我们可以在不传递任何参数的情况下定义箭头函数。

```
const logHelloWorld = () => console.log('Hello World! 🌎')logHelloWorld();
// Hello World! 🌎
```

示例 2:带有单个参数的 Arrow 函数。

```
const logNumber = number => console.log(number)logNumber(42)
// 42
```

正如你所看到的，我们在定义论点时，没有使用括号。如果在箭头函数中使用单个参数，可以省略括号。

**例子 3:多行箭头函数**

到目前为止，我们已经发现了单行箭头函数的用例，但是如果我们需要在函数体中使用另一种逻辑呢？

```
const multiply = (x,y) => {
  console.log(x)
  console.log(y)
  return (
    x*y
  )
}multiply(4,2)
// 4
// 2
// 8
```

正如你在箭头函数定义后看到的，我们把我们的语句放在花括号`**{}**` 中，我们可以这样使用我们的函数。

**例 4:带箭头函数的表达式**

```
const isBiggerThan100 = (number) => number > 100 ? true : false;isBiggerThan100(42) 
// false
```

如您所见，我们已经创建了一个函数，并使用三元运算符来检查数字是否大于 100，如果大于，则返回 true，否则返回 false。

## 箭头函数中的参数绑定

在常规函数中，如果我们在定义函数时没有为函数定义任何参数，我们仍然可以访问函数的参数:

```
function testArguments() {
    console.log(arguments)
}testArguments(1,2,3)// Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

如果我们试图用箭头函数做同样的事情，我们真的做不到。

```
const testArguments = () => {
    console.log(arguments)
}testArguments(1,2,3)
// Uncaught ReferenceError: arguments is not defined
```

当我们试图在这里记录参数时，我们将得到 ReferenceError。

有一种方法可以通过扩展语法来实现这一点。

```
const testArguments = (...n) => {
    console.log(n)
}testArguments(1,2,3)
// [1, 2, 3]
```

这和参数并不完全一样，但是如果你想在函数中使用 n 个参数，你可以这样做。

## 在箭头函数中使用此关键字

在常规函数中使用这个关键字指的是调用它的函数。

另一方面，arrow 函数没有这个关键字，它总是引用父作用域。

```
function Person() {
    this.name = 'Jack',
    this.age = 25,
    this.sayHello = function () {
      // this is accessible
      console.log('Hello', this.name);
      function innerFunction() { // this refers to the global object
        console.log(this.age);
        console.log(this);
      } innerFunction();   }
}let x = new Person();
x.sayHello()// Hello Jack
// undefined
// Window {window: Window, self: Window, document: document, name: '', location: Location, …}
```

正如你在这里看到的，我们的 sayHello 函数正确地写了 this.name，但是当我们试图访问 this.age 时，我们不能使用 age，因为它引用了 **innerFunction** 本身。

现在，如果我们将 innerFunction 更改为箭头函数，它将能够使用父作用域。

```
unction Person() {
    this.name = 'Jack',
    this.age = 25,
    this.sayHello = function () {
      // this is accessible
      console.log('Hello', this.name);
      const innerFunction = () => {
        // this refers to the global object
        console.log(this.age); // 25
        console.log(this); // References Person 
      }
      innerFunction(); 
   }
}
let x = new Person();
x.sayHello()// Hello Jack
// 25
// Person {name: 'Jack', age: 25, sayHello: ƒ}
```

这里，我们与 arrow 函数一起使用的内部函数访问了**的父作用域**，因此我们可以访问`this.age`和`this`关键字，打印出 Person 函数本身。

仅此而已:)

*如果你觉得这篇文章很有帮助，你* [***可以通过使用我的推荐链接注册一个***](https://medium.com/@melihyumak) **[***中级会员来访问类似的***](https://melihyumak.medium.com/membership) *。***

***跟我上*** [**推特**](https://twitter.com/hadnazzar)

[![](img/c012fae801a3ab846a63dc560d09ff17.png)](https://www.youtube.com/c/TechnologyandSoftware)

Subscribe for more on [**Youtube**](https://www.youtube.com/c/TechnologyandSoftware?sub_confirmation=1)

# 编码快乐！

梅利赫

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*