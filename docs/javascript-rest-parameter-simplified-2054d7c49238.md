# 简化的 JavaScript Rest 参数

> 原文：<https://javascript.plainenglish.io/javascript-rest-parameter-simplified-2054d7c49238?source=collection_archive---------13----------------------->

## 深入探究 rest 参数——理解为什么以及如何使用它们。

![](img/0a41ca0989783e7ae29ccb7a1d829c68.png)

Photo by [Sincerely Media](https://unsplash.com/@sincerelymedia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

ES6 引入了几个特性，让 JavaScript 开发人员的生活变得更加简单。其中一个特性是 rest 参数。今天，在本文中，我们深入研究 rest 参数，并试图理解如何使用它们以及为什么要使用它们。

那么，我们开始吧。

## **什么是休息参数？**

顾名思义，rest 参数用于访问传递给函数的参数，并对传递的参数进行任何操作。

在使用 rest 参数之前，开发人员习惯使用 arguments 对象进行相同的操作。让我们看看这个 arguments 对象是什么，以及为什么使用 rest 参数比 arguments 对象更好。

请看下面的片段:

```
function argumentExample(a, b) {console.log('Value of A', a);console.log('Value of B', b);console.log('Value of C', arguments);}argumentExample(1, 2, 3, 4);Value of A 1
Value of B 2
Value of C [Arguments] { '0': 1, '1': 2, '2': 3, '3': 4 }
```

因此，正如你所看到的，arguments 变量保存了传递给函数的所有参数。现在，问题可能会出现，如果我们已经有了这个 arguments 对象，那么使用 rest 参数的目的是什么。

因此，以下是 arguments 对象的一些缺点:

1.  arguments 对象保存所有传递的参数(一个赋给变量，另一个赋给左边的变量)。因此，如果需要获得关于其余参数的信息，我们必须进行额外的计算。
2.  默认情况下，arguments 对象无权访问数组方法/属性。因此，如果我们不得不对参数迭代地执行任何操作，那么它们将会失败。

```
function argumentExample(a, b) {console.log('Value of A', a);console.log('Value of B', b);console.log('Value of C', typeof arguments);arguments.map((elem) => {console.log(elem);});}argumentExample(1, 2, 3, 4);
```

在这里，如果我们尝试使用带有参数的 map 操作符，我们将得到如下所示的错误:

```
TypeError: arguments.map is not a function
    at argumentExample (D:\Blog_Topic\Destructure\rest.js:13:13)
    at Object.<anonymous> (D:\Blog_Topic\Destructure\rest.js:18:1)
    at Module._compile (node:internal/modules/cjs/loader:1103:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1157:10)
    at Module.load (node:internal/modules/cjs/loader:981:32)
    at Function.Module._load (node:internal/modules/cjs/loader:822:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:77:12)
    at node:internal/main/run_main_module:17:47
```

剩下的唯一解决方案是首先将参数转换为数组。

3.arguments 对象在 arrow 函数中不能很好地工作。

```
const argumentExample = (a, b) => {console.log('Value of A', a);console.log('Value of B', b);console.log('Value of C', arguments);};argumentExample(1, 2, 3, 4);Value of A 1
Value of B 2
Value of C [Arguments] {
  '0': {},
  '1': [Function: require] {
    resolve: [Function: resolve] { paths: [Function: paths] },
    main: Module {
      id: '.', .....
```

在上面的代码片段中，arguments 对象的值是一些奇怪的值。

基本上，箭头函数没有自己的参数对象。它们可以访问最近的非箭头父函数的 arguments 对象，因此这里输出了相同的值。

为了避免上面提到的缺点，最好改用 rest 参数。让我们详细了解一下。

**基本用法**

```
function restExample(a, b, ...c) {   
console.log('Value of A', a);
console.log('Value of B', b);
console.log('Value of C', c);
}
restExample(1, 2, 3, 4);
// Output
Value of A 1
Value of B 2
Value of C [ 3, 4 ]
```

在函数定义中，我们将函数参数定义为(a，b，…c)。这里(…c)是我们定义 rest 参数的方式，即三个点后跟变量名。在幕后，JavaScript 将参数一对一地分配给函数中传递的参数，一旦遇到 rest 参数，它就将所有其余的参数分配给用变量名定义的变量。

这里需要注意的重要一点是，rest parameter 可以访问数组属性和方法，因此可以利用它们来进行任何计算。让我们来看一个片段:

```
function restExample(a, b, ...c) {console.log('Value of A', a);console.log('Value of B', b);c.map((elem) => {console.log('Elem', elem);});}restExample(1, 2, 3, 4);Value of A 1
Value of B 2
Elem 3
Elem 4
```

## **使用 rest 参数时的一些问题**

**rest 参数应该是你的最后一个参数:**

```
function restExample(a, ...c, b) {console.log('Value of A', a);console.log('Value of B', b);c.map((elem) => {console.log('Elem', elem);});}restExample(1, 2, 3, 4);function restExample(a, ...c, b) {
                            ^SyntaxError: Rest parameter must be last formal parameter
```

如果我们试图在中间使用 rest 参数，我们将遇到一个错误，解释它应该是最后一个参数。

**函数中必须有一个 rest 参数:**

```
function restExample(...a, ...c) {console.log('Value of A', a);console.log('Value of B', c);}restExample(1, 2, 3, 4);function restExample(...a, ...c) {
                         ^SyntaxError: Rest parameter must be last formal parameter
```

在上面的例子中，我们尝试使用 2 个 rest 参数，但是在那种情况下，我们也收到了一个错误。

简而言之，这就是 rest 参数。希望你现在能更好地理解它。如果您有任何疑问或担忧，请在回复中告知我。

关于我——我是一个编程爱好者，喜欢阅读和写作前端设计、JavaScript 和 UI/UX 相关的东西。点击[这里](https://medium.com/@avinash.dev21987)阅读我所有的文章，并让我知道你的反馈。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*