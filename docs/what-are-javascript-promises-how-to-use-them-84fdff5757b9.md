# 什么是 JavaScript 承诺&如何使用它们

> 原文：<https://javascript.plainenglish.io/what-are-javascript-promises-how-to-use-them-84fdff5757b9?source=collection_archive---------9----------------------->

## 什么是承诺，为什么要使用承诺？

![](img/68a5282e321580cf72b819546b7c9cb9.png)

Photo by [alise storsul](https://unsplash.com/@alisestorsul?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/pinkie-promise?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# Javascript 的问题

JavaScript 有一个问题:它是单线程的。

我们这样说是什么意思？如果某件事需要时间，JS 引擎在此期间不能做任何其他事情。

有时候，当编写“while”代码块时，我会忘记在结束条件中增加变量。这就产生了一个无限循环。当我这样做的时候…一切都冻结了。浏览器不再响应。我不得不强行关上窗户。这是一个极端的例子。但是让我们退后一点。电影以每秒 24 帧的速度运行，视频游戏以每秒 60 帧或更高的速度运行。每秒 24 帧意味着每 40 毫秒左右一帧。(1/24 = 0.0416 秒)。

对于流畅的体验，JavaScript 中的任何进程都必须在 40 毫秒或更短时间内完成任务。否则，用户会觉得应用程序落后了。

如果你想调用一个 web 服务器上的 API，消息的往返肯定要比这个时间长。但是浏览器等不起。

所以我们需要找到方法告诉代码在等待的时候做其他的事情。

# 回调函数

第一个解决方案是告诉浏览器:“运行这个过程(例如，调用这个 API)，当它完成时，让我知道”。或者更准确地说:在完成时执行所提供的函数(作为函数调用中的一个参数)。我们希望代码回调的这个函数就是所谓的…回调。

这个回调函数允许我们添加更多的逻辑来响应服务器的响应。例如:当用户点击按钮时，首先通过调用登录 API 进行登录。当服务器响应时，检索身份验证数据并解释它。然后用登录数据调用 web 服务来更新玩家的信息。

仅在这个例子中，就有三个回调在起作用。第一个响应按钮的按下。第二个管理对登录 API 的调用和响应。最后一个从第二个 web 服务中检索响应。记住这个例子既不牵强也不复杂。

但是这种过程会在回调中产生回调。代码很快变得不可读，它产生“回调地狱”。

这种操作还会带来另一个问题:错误处理。

假设您在回调堆栈的每个阶段或深度都要执行特定的处理。现在想象一个错误发生了。如果它不是用 try/catch 管理的，则错误消息是无用的。“匿名函数的第 5 行出现错误”。

这甚至还没有触及代码无声地失败的情况。

唯一的解决方案是在每个深度、每个回调调用上添加 try/catch 管理。这很快变得很难操作。

# 什么是承诺？

为了解决这些问题，发明了一种新的物体。它有三个基本属性:

1.  它封装了异步处理
2.  它可以被链接，不需要嵌套(回调)函数。
3.  它处理错误

这个对象就是承诺。

一个承诺有两个可以调用的功能:“然后”和“抓住”。“then”函数将解析的结果作为参数，并返回一个新的承诺。“catch”函数将*误差*作为参数，并返回一个新的承诺。

这些函数返回承诺的事实正是允许我们“链接”它们的原因，即:

```
p.then(function1).then(function2)
```

其中`p` 是一个承诺。链接允许我们顺序读取代码，而不是越来越深地陷入嵌套的回调函数。

无论哪一步出错，承诺都会触发第一个“catch”。这允许集中(和理智！)错误管理。

# 如何做出承诺

让我们编写一个函数，创建一个等待指定时间的承诺。让我们称这个函数为 sleep。

Promise 的构造函数接受一个函数。

该函数将两个函数作为参数，通常称为“resolve”和“reject”。当过程结束时我们称之为。要么成功，在这种情况下我们称之为“解决”，要么失败，我们称之为“拒绝”。

我们的睡眠功能看起来像这样:

```
const sleep = (nb) => {
  return new Promise ((resolve, reject) => {
    setTimeout(() => resolve(), nb) ;
  })
};
```

这里没有使用第二个参数 reject。我们可以省略它，但为了完整起见，我们会保留它。如果我们这样做了:

```
sleep(1000).then(() => console.log("done")); 
```

睡眠产生一个承诺，在一定时间后触发一个功能。

# 承诺是好的，但我们可以做得更好！

我有好消息。有一种更好的方式来称呼承诺。

这可能感觉不同，因为“then”函数从未被显式调用。相反，这种语法依赖于 async/await 关键字。但它所做的只是让我们称之为承诺。它是如何工作的？

好吧，让我们用睡眠承诺来举一个基本承诺序列的例子:

```
const wait = () => {
  sleep(1000)
    .then(() => sleep(1000))
    .then(() => console.log(“2s later”);
} ;
```

使用 async/await 符号，我们可以写同样的东西:

```
const wait = async () => {
  await sleep(1000);
  await sleep(1000);
  console.log(“2s later”) ;
} ;
```

只有语法上的区别。正在调用相同的 Promise 对象。如果我们将两个 await 调用包装在 try/catch 中，它将像同步代码一样处理错误。

所有这些都改变了写承诺的方式。这非常类似于我们编写同步代码的方式。即使我们实际上在喊承诺。上面定义的等待函数也返回一个承诺。

# 概括起来

JavaScript 完全是关于与接口和 API 的交互。回调曾经是这样做的首选方式，但是它们有很多缺点。承诺是一个更好的解决方案。async/await 语法使用 Promises 来描述异步行为，同时保持可读性。并让我们逃离“回调地狱”。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***