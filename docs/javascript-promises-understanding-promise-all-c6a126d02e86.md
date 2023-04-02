# JavaScript Promises:了解 Promise.all()

> 原文：<https://javascript.plainenglish.io/javascript-promises-understanding-promise-all-c6a126d02e86?source=collection_archive---------5----------------------->

![](img/9cda5ea26c2b01abc1c2320806f44316.png)

Photo by [Artem Sapegin](https://unsplash.com/@sapegin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

ECMAScript 2021 是最新的 JavaScript 版本，它为 JavaScript 语言引入了多个新特性。但是 promise.all()是在 ECMAScript 2015(ES6)中引入的，有效期为 7 年。

在本文中，我们将看看`promise.all()`是如何工作的，以及我们如何一次执行多个异步调用。

# Promise.all()方法

`Promise.all`方法接受一个可迭代的承诺(接受一个承诺数组)并返回一个包含输入承诺结果数组的新承诺。
同时并行处理多个承诺，并等待所有承诺就绪。

语法:-

```
const data = Promise.all([promise1, promise2,...]); // iterable
```

您可以使用**提取承诺解析值。然后**语法:-

```
data.then((values) => {
  values; // [resultOfPromise1, resultOfPromise2, ...]
}).catch(error => {
  console.log(error)
}
```

或者**异步/等待**:

```
try{
 const result = await data;
 console.log(Result); //[resultPromise1, resultPromise2, ...]
} catch (error => {
 console.log(error);
}
```

请注意，结果数组的顺序与其源承诺中的顺序相同。

关于 `promise.all()` 有趣的事情是:-

*   如果所有承诺都成功解析，那么结果将由包含每个承诺值的结果数组组成。
*   但是如果任何一个承诺被拒绝，那么由`promise.all()`返回的承诺会立即被拒绝，并出现错误。

我举个例子让你更好的理解以上两点:

**示例 1:-**

正如你所看到的，承诺的结果和它的源承诺顺序相同。尽管第一个承诺需要最长的时间来解决，但它仍然是一系列结果中的第一个。

**示例 2:-**

这里第二个承诺两秒后拒绝，导致`promise.all()`立即拒绝，所以**。catch** 执行。即使其中一个失败，另一个仍将继续执行，但它们的结果将被忽略。

# 结论:-

`Promise.all()`是一个有用的函数，可以并行执行多个异步操作，并将结果聚合到一个数组中。

它接受一个**可迭代对象**，比如一个承诺数组作为输入。

*   如果所有的承诺都兑现了，我会得到结果。
*   如果任何一个承诺被拒绝，就会被拒绝。
*   当涉及多个异步任务时经常使用。
*   这个方法**聚合了多个承诺的结果**。

[**浏览器兼容性**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all#browser_compatibility)
请注意，`promise.all()`在除了 internet explorer 之外的所有现代浏览器中都完全支持。

这将是一系列文章，在下一篇文章中我们将讨论 promise.any()。敬请期待！！！

> 请在评论区分享你的观点，是的，欢迎反馈。
> 希望你会喜欢并分享这篇文章，以便更好地到达
> 查看我的其他文章在——[**https://medium.com/@aayushtibra1997**](https://medium.com/@aayushtibra1997) **感谢阅读:)**

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***