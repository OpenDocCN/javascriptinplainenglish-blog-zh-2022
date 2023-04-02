# JavaScript:如何使用 Promise.race()

> 原文：<https://javascript.plainenglish.io/javascript-how-to-use-promise-race-1c3d552afc0b?source=collection_archive---------3----------------------->

![](img/54a175a1a69130febdd617b54fa1ead4.png)

Photo by [Zachary Nelson](https://unsplash.com/@zach_codes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是世界上最流行的编程语言之一，因为它能够实现异步编程。承诺是这个概念的核心，在本文中，我们将探索如何使用`Promise.race()`方法。

## 介绍

当异步执行代码时，它可以通过允许同时执行其他代码来提高性能。承诺是 JavaScript 中异步编程的关键部分，它们有助于管理异步工作。

通过利用 JavaScript 的能力，开发人员找到了提高效率的方法。例如，`Promise.race()`方法允许开发人员在多个承诺之间创建异步竞赛。该方法返回一个将解决或拒绝的承诺，这取决于 iterable 中要解决的第一个承诺的最终状态。

## 句法

`Promise.race()`方法的语法如下:

```
Promise.race(iterable);
```

这个方法接受一个可重复的承诺，并返回一个承诺。该方法执行一场“比赛”，其中每个承诺将并行运行。如果第一个要完成的承诺被解析，那么返回的承诺也用该承诺的值进行解析。否则，如果第一个要完成的承诺拒绝，那么返回的承诺也拒绝，原因来自该承诺。

![](img/872384ca6f2bd3587ce00f120c23ae08.png)

Photo by [Max Duzij](https://unsplash.com/@max_duz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 例子

让我们看一个简单的例子来理解这是如何工作的:

```
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 1 resolved');
  }, 5000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 2 resolved');
  }, 1000);
});

Promise.race([promise1, promise2]).then(value => {
  console.log(value); // expected output: "Promise 2 resolved"
});
```

在这个例子中，我们有两个承诺，promises 1 和 promises 2。承诺 1 五秒后解决，承诺 2 一秒后解决。当我们将它们传递给`Promise.race()`方法时，它将并行运行承诺，并返回一个用第一个要解决的承诺的值解决的承诺。在这种情况下，promise2 将首先解析，因为它的超时比 promise1 短。

## 结论

`Promise.race()`方法是 JavaScript 中异步编程的强大工具。它允许开发人员在多个承诺之间创建异步竞争，并根据第一个解决的承诺的状态返回解决或拒绝的单个承诺。希望这篇文章教会你一些东西！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***