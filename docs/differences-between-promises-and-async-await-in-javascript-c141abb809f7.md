# JavaScript 中承诺和异步/等待的区别

> 原文：<https://javascript.plainenglish.io/differences-between-promises-and-async-await-in-javascript-c141abb809f7?source=collection_archive---------1----------------------->

## **异步/等待**和**承诺有什么区别？**

![](img/365981385af8e391a78f48d8087f2667.png)

JavaScript

# JavaScript 中 async/await 和 promises 的区别——面试问题 11

**异步/等待**和**承诺有什么区别？**

大家好，在本教程中，我们将通过**示例了解 **async/await 结构和【promises 之间的区别。****

JavaScript 架构中广泛使用承诺来管理同步流程。在 async-await 关键字的帮助下，JavaScript 世界中加入了一种新的语法糖。

如果你对 promises 和 async-await 的内容不是很熟悉，我建议你阅读下面我写的解释 **promises** 和 **async/await** 的文章。

[](https://melih193.medium.com/javascript-promises-javascript-interview-questions-9-94b2c4bc19f1) [## Javascript 承诺:Javascript 面试问题 9

### javascript 中的承诺——面试问题 9——什么是承诺，我们如何在 javascript 中使用承诺？

melih193.medium.com](https://melih193.medium.com/javascript-promises-javascript-interview-questions-9-94b2c4bc19f1) [](https://medium.com/codex/javascript-async-await-javascript-interview-questions-10-e51629bef827) [## Javascript 异步/等待:Javascript 面试问题#10

### javascript 中的 Async/Await——面试问题 10——什么是 async/Await，我们如何使用 async……

medium.com](https://medium.com/codex/javascript-async-await-javascript-interview-questions-10-e51629bef827) 

如果你知道关于 JavaScript **promises** 和 **async/await** 关键字的所有概念，现在我们可以开始看看它们之间的区别了。

## 承诺和异步/等待之间的区别

注意:下面的列表可以与下面描述的数字相匹配。

## **承诺**

1.承诺代表保证完成执行的过程。

2.承诺有 3 种状态，这些状态是**待定、已解决、**和**拒绝。**

3.如果承诺被**锁住。然后()，**将函数添加到回调链后继续执行。

4.可以使用**进行错误处理。然后()**和**。catch()** 方法。

5.承诺链可能难以理解和遵循。

6.多重承诺链的调试可能非常棘手。

7.承诺可用于承诺链中的多个承诺。

## 异步/等待

1.Async await 是承诺的语法糖。让代码看起来像是同步执行的。

2.异步 await 没有状态。异步函数返回一个承诺。这种承诺状态可以被解决，也可以被拒绝。

3.Await 挂起被调用函数的执行，直到 promise 返回该执行的结果。如果在 await 之后调用了其他函数，这些执行将一直等到 promise 完成。

4.错误处理可以用 try-catch 块来完成。

5.Async/Await 使得读取承诺流更加容易。与承诺相比，理解功能也非常容易。

6.使用 async/await 进行调试要容易得多。

7.Await 可用于单个承诺或 promise.all()。

## 你应该使用承诺还是异步/等待？

这是一个非常普遍的问题，在编写 JavaScript 代码时，我们可能需要使用这两种情况。承诺和 async-await 密切相关。

*   如果您正在使用依赖于第一个异步函数的另一个异步函数，您应该使用 await 来等待第一个异步函数完成，而不是使用承诺链。
*   Await 关键字会阻止下一行的执行，直到它完成。如果你不需要阻止执行，你可以调用异步函数而不需要等待。(**例如，** push notifications，如果你不想检查 push notification 的状态是否已经发送，你可以跳过 await 关键字，代码将异步继续执行)
*   如果有多个异步函数可以并行运行，可以使用 **promise.all([promise1，promise2])** 在**并行运行。**
*   使用 async/await 肯定会帮助您更快地理解异步流程。
*   与使用承诺链不同，async / await 提供了更简洁的代码。
*   如果您正在使用许多微服务和异步函数，使用 async / await 将帮助您更快地调试代码。在承诺链中生成断点可能非常棘手。
*   Async await 使异步代码看起来像同步代码。
*   要发现承诺中的错误，总是需要你写下**。catch()** 块。
*   Async await 可以和所有其他代码一起写在 try-catch 块中。

## 结论:

在处理承诺时使用 async / await 带来了如此大的灵活性、干净的代码和更容易的调试。

除了使用 Promise.all()运行并行异步执行之外，您可以使用 async / await 完成所有其他异步任务。

使用 async/await 肯定会在你从事大型项目时给你带来很多好处，它会让你和其他开发人员的生活变得轻松。

这就是关于 **async/await 的全部内容，并承诺在 JavaScript 中进行比较。**

我希望在你读完这篇文章后，你能回答所有的 **JavaScript** **承诺和异步/等待面试问题**。

*如果您觉得这篇文章很有帮助，您可以通过使用我的推荐链接注册一个* [***中级会员来访问类似的文章***](https://melihyumak.medium.com/membership) *。*

***跟我上*** [**推特**](https://twitter.com/hadnazzar)

[![](img/c012fae801a3ab846a63dc560d09ff17.png)](https://www.youtube.com/c/TechnologyandSoftware)

Subscribe for more on [**Youtube**](https://www.youtube.com/c/TechnologyandSoftware?sub_confirmation=1)

# 编码快乐！

梅利赫

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/)***[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。****