# JavaScript 承诺:它们是什么以及如何使用它们

> 原文：<https://javascript.plainenglish.io/javascript-promises-what-they-are-and-how-to-use-them-fe5b55496271?source=collection_archive---------8----------------------->

![](img/fdfd87987c009fcfcca7439888ba7607.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

promises——2015 年加入 JavaScript 的新特性。它们旨在使异步编程更容易、更可靠。在这篇博文中，我们将讨论 JavaScript 承诺是什么，以及如何在自己的代码中使用它们。

## 什么是 JavaScript 承诺？

JavaScript Promise 是一个表示未来值的对象。异步编程中使用承诺来处理需要时间才能完成的操作的结果。例如，当您发出网络请求时，请求需要一些时间才能完成。JavaScript Promise 对象允许您编写将在请求完成时执行的代码。

承诺有三种状态:待定、履行和拒绝。首次创建承诺时，它处于待定状态。这意味着操作尚未完成。一旦操作完成，承诺要么被履行，要么被拒绝。完成的承诺意味着操作成功，承诺的 value 属性将包含操作的结果。被拒绝的承诺意味着操作失败，承诺的 value 属性将包含一条错误消息。

## 为什么要创建 JavaScript 承诺？

JavaScript 的出现是为了让异步编程变得更容易。在承诺之前，开发人员必须使用回调函数来处理异步操作的结果。回调函数很难调试，可能会导致代码难以阅读。对异步代码使用回调函数也会导致回调地狱。回调地狱是指开发人员不得不将回调函数嵌套在彼此内部。当需要依次执行多个异步操作时，就会发生这种情况。JavaScript 承诺提供一种更直接的方式来编写异步代码。

## 如何用 then()处理兑现的承诺

一旦实现了 JavaScript 承诺，就会执行承诺的 then()方法中的代码。then()方法有两个参数:一个用于成功操作的回调函数和一个用于失败操作的回调函数。这些回调函数被称为履行处理程序和拒绝处理程序。履行承诺时调用履行处理程序，拒绝承诺时调用拒绝处理程序。在大多数情况下，您只需要提供一个实现处理程序，因为您可以使用 catch()方法来处理被拒绝的承诺。

以下示例显示了如何处理已履行的承诺:

```
let promise = makeAsyncRequest();promise.then(function(result) { // Handle successful result}, function(error) { // Handle error});
```

在上面的例子中，makeAsyncRequest()函数发出一个异步请求并返回一个承诺。当请求完成时，执行 then()方法中的代码。如果请求成功，操作的结果被传递给第一个回调函数。如果请求失败，错误消息将被传递给第二个回调函数。

需要注意的是，承诺总是异步的。这意味着在 Promise 的 then()方法中编写的代码不会立即执行。为了异步执行代码，它必须放在回调函数内部。

![](img/86ab380a50701138f426e3252b1fd72f.png)

Photo by [Alex Kotliarskyi](https://unsplash.com/es/@frantic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 如何用 catch()处理被拒绝的承诺:

如果 JavaScript 承诺被拒绝，将执行 catch()方法中的代码。catch()方法有一个参数:失败操作的回调函数。这个回调函数被称为拒绝处理程序。当承诺被拒绝时，将调用拒绝处理程序。

以下示例显示了如何处理被拒绝的承诺:

```
let promise = makeAsyncRequest();promise.then(function(result) { // Handle successful result}).catch(function(error) { // Handle error});
```

在上面的例子中，makeAsyncRequest()函数发出一个异步请求并返回一个承诺。当请求完成时，执行 then()方法中的代码。如果请求成功，操作的结果被传递给回调函数。如果请求失败，将向 catch()方法传递一条错误消息。

## JavaScript 承诺摘要

以下是我们所学内容的总结:

*   承诺可以是三种状态之一:待定、履行或拒绝。
*   待定承诺意味着操作尚未完成。
*   实现的承诺意味着操作成功，并且承诺的 value 属性包含操作的结果。
*   被拒绝的承诺意味着操作失败，并且承诺的 reason 属性包含错误消息。
*   您可以使用 then()方法处理履行的承诺，使用 catch()方法处理拒绝的承诺。
*   在 Promise 的 then()或 catch()方法中编写的代码不会立即执行。为了异步执行代码，它必须放在回调函数内部。

您可以使用 JavaScript 编写更简单、更可靠的异步代码。我希望你从这篇文章中学到了一些东西，祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*