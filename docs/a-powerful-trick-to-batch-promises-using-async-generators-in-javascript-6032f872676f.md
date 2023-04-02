# 在 JavaScript 中使用异步生成器批量承诺的强大技巧

> 原文：<https://javascript.plainenglish.io/a-powerful-trick-to-batch-promises-using-async-generators-in-javascript-6032f872676f?source=collection_archive---------8----------------------->

## 关于如何在 JavaScript 中使用异步生成器批量承诺的教程。

![](img/178f4780a6daecf0af5e6976c68316ef.png)

Photo by [Aaron Thomas](https://unsplash.com/@aaronphs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@aaronphs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当您必须迭代一个集合并在每次迭代中执行昂贵的异步任务时，批处理非常有用。[异步发生器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of#iterating_over_async_generators)使得这个非常容易实现。

在这个例子中，我们将查看一个简单的带有可调整并发限制(一次批处理的任务数)的数组块批处理。我们将使用名为`Task`的类型来表示返回`[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)`的异步计算。

`Task`是任何返回承诺的函数。承诺并不是天生懒惰的，它们一建立起来就开始执行。将它们封装在一个函数中，可以让我们控制何时执行这个承诺。

# 实施:

*   给定一个数组`Tasks`，我们想要在我们的并发限制(批处理大小)的“步骤”中迭代它，我们将为此使用一个简单的 for 循环。
*   我们希望能够并发执行该批任务并等待它们。我们可能需要使用`[Promise.all](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)`方法，在异步函数和`await`批处理任务的执行上下文中完成。
*   可选地，我们想要附加一个回调，当我们的任务批处理成功时，我们可以调用这个回调。
*   最后，当一批任务完成时，我们希望通知消费者任务已经完成，这样他们就可以继续他们的异步迭代。

这最后一点是`[Async Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)`可以帮助我们变魔术的地方！他们允许我们在异步生成器函数中使用`await`语法(使用`async function*`语法声明)。这就释放了异步迭代承诺并一个接一个地`await`它们的能力。

下面是我们计划的执行情况:

`[Async Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)`也让我们`yield`将这些期待的值传递给生成器函数的消费者。这允许他们使用简洁的`[for await (...)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of)`循环语法异步迭代数据🎉

这个堆栈展示了我们的任务批处理程序的一个简单实现。尽情享受吧！

您可以进一步使用基于池的方法进行批处理，使用`[Promise.race](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)`方法来检测和填充任务池中的空白点。:D

请随时联系我，让我知道它是如何为你工作的；)

快乐工程！

***如需更多此类文章更新请订阅*** [***我的免费简讯***](https://www.bytelimes.com/#/portal/signup/free) ***。***

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***