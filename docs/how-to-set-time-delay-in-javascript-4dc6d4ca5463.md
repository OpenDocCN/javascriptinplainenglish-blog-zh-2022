# 如何在 JavaScript 中设置时间延迟？

> 原文：<https://javascript.plainenglish.io/how-to-set-time-delay-in-javascript-4dc6d4ca5463?source=collection_archive---------1----------------------->

## 关于如何在延迟后运行 JavaScript 代码的指南。

![](img/f1949b6cca4f970584bceff967ef3901.png)

Photo by [Johnny Cohen](https://unsplash.com/@jonecohen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在延迟之后运行一些 JavaScript 代码。

在本文中，我们将了解如何在 JavaScript 中设置时间延迟。

# 使用 setTimeout 方法

我们可以使用`setTimeout`方法在延迟一段时间后运行代码。

例如，我们可以写:

```
setTimeout(() => {
  console.log('hello world')
}, 1000);
```

我们将延迟后运行的回调作为第一个参数传入。

我们将等待回调运行的延迟以毫秒为单位作为第二个参数。

现在我们应该看到 1 秒钟后记录的`'hello world'`。

# 在承诺中使用 setTimeout 函数

我们可以在一个承诺中使用`setTimeout`函数，这样我们就可以很容易地连续多次使用`setTimeout`。

为此，我们写道:

```
const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms));
}(async () => {
  console.log("Hello");
  await sleep(2000)
  console.log("world");
})()
```

我们创建了`sleep`函数，它返回用`Promise`构造函数创建的承诺。

我们传入一个接受`resolve`函数并使用`resolve`函数调用`setTimeout`的回调，以便解析承诺。

`ms`是等待`resolve`运行的延迟时间，单位为毫秒。

然后我们可以在下面的`async`函数中使用它。

因此，我们应该首先看到记录的`'Hello'`。

2 秒钟后，`'world'`被记录。

# 结论

我们可以用`setTimeout`方法运行有时间延迟的代码。

要按顺序使用，我们可以把它包在一个承诺里。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的**[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***