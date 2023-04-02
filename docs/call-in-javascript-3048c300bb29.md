# JavaScript 中调用的介绍

> 原文：<https://javascript.plainenglish.io/call-in-javascript-3048c300bb29?source=collection_archive---------13----------------------->

## 理解' ***的概念在 JavaScript 中调用'*** ，用来轻松实现某些功能。

![](img/8e0fc875d02ebfb659022fb16fea1127.png)

Photo by [Alexander Andrews](https://unsplash.com/@alex_andrews?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我们将刷新 JavaScript 中的一个核心概念，即 ***调用*** ，如果使用得当，可以使实现某些功能变得更加容易。

为了再次理解致电，我们将使用**为什么以及如何接近**。

## 在“为什么我们会看到使用案例为什么要使用呼叫”和“我们将如何看到如何使用呼叫”中。

那么，让我们从这个问题开始，为什么要使用 call？

假设，我们有几个对象，比如:

```
const objOne = {firstName: 'Virat',lastName: 'Kohli',};const objTwo = {firstName: 'Rohit',lastName: 'Sharma',};
```

现在，假设我们想以某种格式获取名字和姓氏，如何实现呢？

一个直接的解决方法是给每个对象添加单独的函数，如下所示:

```
const objOne = {firstName: 'Virat',lastName: 'Kohli',fullName: function () {return `First Name - ${this.firstName} , Last Name - ${this.lastName}`;},};const objTwo = {firstName: 'Rohit',lastName: 'Sharma',fullName: function () {return `First Name - ${this.firstName} , Last Name - ${this.lastName}`;},};console.log(objOne.fullName()); /// First Name - Virat , Last Name - Kohliconsole.log(objTwo.fullName()); // First Name - Rohit , Last Name - Sharma
```

很简单，没错，而且它也在工作。大团圆结局！今天到此为止。😏不完全是。上述实现存在一些问题。

*   违反 DRY 原则:我们在每个对象中重复相同的代码块，这违反了编程原则。
*   我们通过在每个对象中添加相同的代码块来增加对象的重量。
*   假设，一段时间后，如果需要改变函数返回类型的格式，我们必须执行更新每个对象的繁琐任务。

有意思！那么，解决办法是什么？

如果您观察上面的函数定义，您可以很容易地看到，对于每个函数，唯一的区别点是对象变量(在我们的例子中是名字和姓氏)，如果我们可以以某种方式将这个对象实例传递给这个函数，我们就可以克服上面列出的所有问题。

但是如何才能实现这一点呢？

来帮忙吧，调用函数，这是 JavaScript 中最简单明了的关键字。相信我，你很快就会意识到这一点。

对于 JavaScript 中的每一个函数，function 的原型都有一个方法调用，它只是用我们想要的相关对象调用函数。

听起来很困惑。

好了，让我们用更简化的方式重写上面的代码块。

```
function fullName() {return `First Name - ${this.firstName} , Last Name - ${this.lastName}`;}const objOne = {firstName: 'Virat',lastName: 'Kohli'};const objTwo = {firstName: 'Rohit',lastName: 'Sharma'};
```

现在，这里我们已经定义了一个全局全名函数，其中我们返回所需的全名的相关格式。

但是如何利用这一点。

如上所述，每个函数原型都有一个调用方法，该方法使用作为第一个参数传入的对象来调用函数。
为了更好地理解，请参考此图示。

![](img/5769bcbb717628c5fbc74d2ce98da276.png)

Call

现在，我们已经定义了函数，但如何使用它。

```
fullName.call(objOne)fullName.call(objTwo)
```

只要用上面的语法调用 fullName，就会发生下面的事情:

*   fullName 被立即调用并执行，也称为**急切执行或急切加载**。
*   **“this”**函数内部引用作为第一个参数传入的对象。

通过实施这种方法，我们已经解决了最初方法中的所有问题。

现在，如果您在上面的图片快照中观察到，还有一个额外的参数，即 param，它是通过调用传递的，指的是我们希望传递给函数的任何运行时参数。

为了理解这一点，让我们稍微改变一下全名函数。

```
function fullName(teamName) {return `First Name - ${this.firstName} , Last Name - ${this.lastName} and plays for ${teamName}`;}
```

现在，这里 fullName 需要一个参数和对象，所以我们相应地改变了函数调用。

```
console.log(fullName.call(objOne, 'RCB'));console.log(fullName.call(objTwo, 'MI'));
```

现在，我们在调用时传入一个参数，在函数的执行过程中将对该参数进行解析，结果输出将是:

```
First Name - Virat , Last Name - Kohli and plays for RCB
First Name - Rohit , Last Name - Sharma and plays for MI
```

这里需要注意的一点是，在函数上使用 call 时，我们也可以将 null 作为第一个参数传递。
**在这种情况下，在非严格模式下，这个函数内部会引用一个全局对象，但在严格模式下，同样会引用 undefined。**

涵盖所有场景的整合示例:

```
var firstName = 'Shreyas';var lastName = 'Iyer';function fullName(teamName) {return `First Name - ${this.firstName} , Last Name - {this.lastName} and plays for ${teamName}`;}const objOne = {firstName: 'Virat',lastName: 'Kohli',};const objTwo = {firstName: 'Rohit',lastName: 'Sharma',};console.log(fullName.call(objOne, 'RCB'));console.log(fullName.call(objTwo, 'MI'));console.log(fullName.call(null, 'KKR'));
```

上述情况下的输出:

```
First Name - Virat , Last Name - Kohli and plays for RCB
First Name - Rohit , Last Name - Sharma and plays for MIFirst Name - Shreyas , Last Name - Iyer and plays for KKR // In non strict mode 
First Name - undefined , Last Name - undefined and plays for KKR // In strict mode
```

那么，这就简单介绍一下 call 的用法。
***在这个 3 部分系列的下一部分中，我们将讨论应用以及更多调用/应用的用例。如果你在评论中有任何疑问或者有任何反馈，请告诉我。***

关于我——我是一个编程爱好者，喜欢阅读和写作前端设计、JavaScript、UI/UX 相关的东西。点击[这里](https://medium.com/@avinash.dev21987)阅读我的所有文章。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***