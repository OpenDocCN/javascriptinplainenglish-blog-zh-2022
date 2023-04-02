# JavaScript 中的高阶函数是什么

> 原文：<https://javascript.plainenglish.io/higher-order-functions-in-javascript-a506fa3fb5e1?source=collection_archive---------18----------------------->

## JavaScript 中高阶函数的介绍

![](img/aa7ebd175dc4ec10a9d9c9979fd287b7.png)

## 函数是对象

在 JavaScript 中，函数是对象。这意味着我们可以用它们做很多事情。我们将简要介绍其中的一些内容。首先，我们可以将它们存储在一个变量中，并创建一个函数表达式，如下例所示。

```
const ourFunctionExpression = function(name) {
  return name;
}ourFunctionExpression("Bob");//Returns ---> 'Bob'
```

在上面的例子中，我们声明了一个名为 *ourFunctionExpression* 的变量，并为其分配了一个匿名函数。这个函数接受一个名为的参数*，并返回它。当函数被调用时，我们传入参数*鲍勃*。我们得到 Bob 作为返回值。*

由于函数是对象，我们也可以将它们存储在数据结构中，比如对象和数组。如下例所示。

```
function ourFunction(num) {
  return num + num;
}ourFunction(5);
//Returns ---> 10const ourArray = [1, 2, ourFunction];ourArray[2];//Returns ---> 
ƒ ourFunction(num) {
  return num + num;
}ourArray[2](5);
//Returns ---> 10
```

在上面的例子中，我们创建了一个名为 *ourFunction* 的函数声明。我们设置了一个名为 num 的参数。该函数使用 *num* 参数返回一个和。当我们调用函数并传入参数 5 时，返回 10。我们继续创建一个名为 *ourArray* 的变量，并给它分配一个数组，数组中的第三个元素是 *ourFunction* 。然后我们使用方括号来访问这个元素。返回函数的声明。接下来，我们再次使用方括号来访问元素，但同时我们也调用它，将 5 作为参数传入。我们得到 10 的返回值，就像我们直接调用函数一样。如果一个函数存储在一个对象中，也可以采用类似的方法，如下例所示。

```
function ourFunction(num) {
  return num + num;
}const ourObject = {
  sum: ourFunction
}ourObject.sum;//Returns --->
ƒ ourFunction(num) {
  return num + num;
}ourObject.sum(5);
//Returns ---> 10
```

## 什么是高阶函数？

既然我们已经熟悉了函数是对象并且可以像 JavaScript 中的值一样对待的事实，我们可以看看 JavaScript 中的高阶函数是什么。高阶函数是将函数作为自变量的函数和/或作为值返回函数的函数。我们将从查看以一个函数作为参数的函数开始。

## 作为参数的函数

我们可以声明函数，然后将这些函数作为参数传递给其他函数。这些函数可以对作为参数传入的函数做它们想做的事情，因为函数只是值。让我们看一个例子。

```
function callGreeting(value) {
  return value();
}function greet() {
  return "Hello";
}callGreeting(greet);
//Returns ---> 'Hello'
```

在上面的例子中，我们创建了一个名为 *callGreeting* 的函数声明。该函数有一个值参数，函数体返回*值*参数。我们接下来创建另一个名为 *greet* 的函数声明。这个函数返回字符串*你好*。我们调用 *callGreeting* 函数，并将*greeting*函数作为参数传入。这变成了值参数，因此它在 *callGreeting* 函数体内被调用。字符串 *Hello* 返回。让我们用另一个例子来巩固这一点。

```
function halve(num) {
  return num();
}function add() {
  return 100 + 100;
}halve(add);
//Returns ---> 200
```

在上面的例子中，我们声明了一个名为 *halve* 的函数，它带有一个名为 *num* 的参数。我们假设 *num* 是一个函数，所以在函数体内我们返回调用这个参数的结果。接下来，我们声明一个名为 *add* 的函数，在这个函数中我们返回 100 加 100 的总和。然后我们调用 *halve* 函数并传入 *add* 函数作为参数。我们返回 200，因为 *halve* 调用 *add* 返回 200。

## 用作返回值

函数也可以将函数作为值返回。我们可以将返回的函数存储在一个变量中，然后调用这个变量。以下是这方面的一个例子:

```
function outer() {
  return function() {
    return "Hello";
  }
}const ourFunction = outer();
console.log(ourFunction);//Returns ---> 
 ƒ () {
    return "Hello";
 }ourFunction();//Returns ---> 'Hello'outer()();
//Returns ---> 'Hello'
```

我们声明一个名为 *outer* 的函数，在函数体内我们返回一个匿名函数，该函数返回字符串 *"Hello"* 。我们创建一个名为 *ourFunction* 的变量，并将调用 *outer* 的结果赋给它。当我们控制台记录我们的函数变量时，我们可以看到匿名函数被返回但没有被调用。我们继续调用*我们的函数*，并返回 *Hello* 。我们还可以通过调用带有两组括号的 *outer* 来获得相同的结果，如示例末尾所示。这不是一种可读性很强的方法，这也是为什么使用变量是首选的原因。

再举一个例子来固化我们的理解。

```
function sum(valOne) {
  return function(valTwo) {
    return valOne + valTwo
  }
}const total = sum(1);
total(5);//Returns ---> 6
//ValOne - 1
```

这次我们声明一个名为 *sum* 的函数。该函数接受一个名为 *valOne* 的参数。该函数返回一个匿名函数，该函数设置一个 *valTwo* 参数。该函数返回 *valOne* 参数和 *valTwo* 参数相加的总和。我们声明一个名为 *total* 的变量，并将调用带有参数 1 的 *sum* 函数的结果赋给这个变量。这将返回对从 *sum* 函数返回的匿名函数的引用。然后，我们通过调用变量 total*来调用这个函数，变量 total* 传递 5 作为参数。我们返回 6， *valOne* 变成 1， *valTwo* 变成 5。

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*