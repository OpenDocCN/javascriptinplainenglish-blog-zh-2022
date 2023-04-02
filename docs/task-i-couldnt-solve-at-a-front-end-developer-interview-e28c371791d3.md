# 我在前端开发人员面试中无法解决的任务

> 原文：<https://javascript.plainenglish.io/task-i-couldnt-solve-at-a-front-end-developer-interview-e28c371791d3?source=collection_archive---------0----------------------->

![](img/6eb0820cc089192021afe4d64288b58e.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大约两年前，我在一家 IT 公司面试。很常见的是，有两个开发人员主动用不同的 JavaScript 任务轰炸我。但是他们中的一个给了我一个任务，我没有足够的时间来解决它。感谢这些开发人员，他们给了我他们的“正确”解决方案。我没有运行它，并且整整两年都忘记了这个任务

几个小时前，我想起了这个情况和这个任务。我打开 JSFiddle 网站，复制了他们发给我的解决方案，然后按下“运行”……你觉得怎么样？答案错了！

我将把任务和他们的解决方案复制到这里。试着猜猜它会在

```
console.log()
```

Wrong solution

这个解决方案有什么问题？

1.  如果你运行它——你会看到第一个字符串有 3 次“Rudolf ”,因为它总是开始迭代相同的循环
2.  请让我们走得更远一些。想象一下，我们的数组存储的不仅仅是 3 条记录，而是数千条记录。你能复制粘贴它并调用

```
Promise.all()
```

如同

```
[fakeAPICall(0), …., fakeAPICall(n)]
```

?

我希望—不:)

我将在下面添加我的解决方案

请随时将您的解决方案发送给我🤓

面试成功！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*