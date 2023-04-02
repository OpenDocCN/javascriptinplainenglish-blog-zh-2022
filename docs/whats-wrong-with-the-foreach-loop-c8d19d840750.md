# forEach 循环有什么问题？

> 原文：<https://javascript.plainenglish.io/whats-wrong-with-the-foreach-loop-c8d19d840750?source=collection_archive---------21----------------------->

![](img/813838fd1701125229a68d0c9193a582.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/loops?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

循环是每个人在开始编程时最先学习的概念之一。在大多数编程语言中，我们有 for 循环、while 循环、do-while 循环等。

在 JavaScript 中你知道哪种 for 循环？

我们有传统的 for 循环、forEach 循环、for…of 循环和 for…in 循环。

有没有尝试过用 forEach 循环执行异步操作？

首先，什么是异步和同步？

异步意味着非阻塞。简单认识一下吧。它不会等到一项任务完成后再去执行另一项任务。同步与此相反。一旦当前任务完成，它将进入下一个任务。

在 JavaScript 中，数据库调用、设置超时等行为是异步的。

让我们进入正题。异步操作中的 forEach 循环有什么问题？

我们举个例子来看。

我们有一个数字数组。我们要做的是为每个数字加 2，并将其推送到另一个数组。为了模拟异步的本质，我们在 setTimeout 中添加了。

你认为输出会是什么？

**它会打印一个空数组**，用**arr**初始化。但是为什么呢？为了理解它，让我们在循环中添加一个控制台，如下所示。

这是输出。

```
[]
3
4
5
6
```

发生的情况是，它在循环完成之前运行了 console.log(arr)(第 19 行)。

为了克服这一点，我们可以使用 for…of 循环。

我们得到了预期的输出。

```
[ 3, 4, 5, 6 ]
```

因此，如果你在迭代地进行异步操作，总是倾向于使用 for… of 循环来避免意外。

希望这对您有所帮助。

编码快乐！

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*