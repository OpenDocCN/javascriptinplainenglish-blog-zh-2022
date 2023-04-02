# 理解 JavaScript 中的 apply()方法

> 原文：<https://javascript.plainenglish.io/apply-in-javascript-1848c41ae5f4?source=collection_archive---------15----------------------->

![](img/bd5b0517d1f39317504ccb4d9e6c4133.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在上一篇[文章](/call-in-javascript-3048c300bb29)中，我们学习了如何在 JavaScript 中使用 call 方法。

今天，我们将向前迈出一步，学习 call 的同级，即 apply。

如果你能理解电话，那么申请对你来说就是小菜一碟。我要求你浏览一遍这篇文章:

[](/call-in-javascript-3048c300bb29) [## JavaScript 中调用的介绍

### 理解 JavaScript 中“调用”的概念，它用于轻松实现某些功能。

javascript.plainenglish.io](/call-in-javascript-3048c300bb29) 

这将有助于你更好地理解申请。

***提醒你一下，call 是在函数上使用的，它将一个对象实例作为参数在调用函数内部引用。***

Apply 的工作方式与 call 完全相同，即如果只传递第一个参数(即对象引用), call 和 apply 的语法完全相同。

```
functionName.call(ObjectInstance which function should refer);
functionName.apply(ObjectInstance which function should refer);
```

我们也将重用前一篇文章中使用的函数和代码来理解 apply。

```
function fullName(teamName) {return `First Name - ${this.firstName} , Last Name - ${this.lastName}`;}const objOne = {firstName: 'Virat',lastName: 'Kohli',};const objTwo = {firstName: 'Rohit',lastName: 'Sharma',};console.log(fullName.apply(objOne));console.log(fullName.apply(objTwo));// Output First Name - Virat , Last Name - Kohli
First Name - Rohit , Last Name - Sharma
```

所以，如果你仔细观察，输出就是我们在使用 call 方法时得到的。

那 call 和 apply 的区别是什么？

差异出现在第二个参数中。在调用中，在第一个参数之后，我们可以传递 n 个参数。

但是，在 apply 的情况下，第二个参数本身是一个数组，可以包含多个值，而不是多个参数。

让我们举个例子来理解同样的道理:

```
function fullName(teamName, country) {return `First Name - ${this.firstName} , Last Name - ${this.lastName} and plays for ${teamName} and represents ${country}`;}const objOne = {firstName: 'Virat',lastName: 'Kohli',};const objTwo = {firstName: 'Rohit',lastName: 'Sharma',};console.log(fullName.apply(objOne, ['RCB', 'INDIA']));console.log(fullName.apply(objTwo, ['MI', 'INDIA'])); // OutputFirst Name - Virat , Last Name - Kohli and plays for RCB and represents INDIA
First Name - Rohit , Last Name - Sharma and plays for MI and represents INDIA
```

现在，让我们看看上面的代码片段中发生了什么。

我们使用`fullName`函数并根据需要应用不同的对象实例，作为第二个参数的一部分，我们传递一个字符串数组。

JavaScript apply 方法的好处是它自动析构数组参数，我们不需要迭代第二个参数并获取单个元素。

因此，在我们的例子中，两个数组元素都可以作为函数参数，因此可以使用。

简单来说，这就是应用方法。

***所有适用于 call 的概念都适用，除了第二个及以后的自变量的区别。***

在这个由 3 部分组成的系列的最后一部分中，我们将研究 bind 方法。
到时候，看丫和开心编码。

关于我——我是一个编程爱好者，喜欢阅读和写作前端设计、JavaScript、UI/UX 相关的东西。点击[此处](https://medium.com/@avinash.dev21987)阅读我的所有文章，并告知我您的反馈。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*