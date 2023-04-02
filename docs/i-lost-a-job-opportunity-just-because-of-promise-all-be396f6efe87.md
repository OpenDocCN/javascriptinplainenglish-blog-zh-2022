# “我失去了一个工作机会，只是因为承诺。所有”

> 原文：<https://javascript.plainenglish.io/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87?source=collection_archive---------0----------------------->

## 一次让我好难过的面试经历。

![](img/b5a76370d1f9b6bb627f3f0db0998ade.png)

这是不久前发生在我朋友身上的一次面试经历。面试官希望他实现`Promise.all`功能。可惜我朋友现场发挥不好，回答不了问题。

面试结束后，面试官很不客气地对他说:“你的 JavaScript 基础不够扎实，对很多 JavaScript 原理了解不够。”

实际上，我对面试官的这种行为感到困惑。无法实现 `**Promise.all**` **是否意味着基础没有掌握？很奇怪，你不觉得吗？**

在接下来的内容中，我试图揭开`Promise.all`和其他重要承诺方法的神秘面纱。所以让我们开始吧。

# 1.承诺。所有

*来自*[*MDN*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)*:*

*" Promise . all()方法将可迭代的承诺作为输入，并返回一个承诺，该承诺解析为输入承诺的结果数组。*

*当输入的所有承诺都实现时，或者如果输入 iterable 不包含承诺，则返回的承诺将实现。*

*当任何输入承诺拒绝或非承诺抛出错误时，它立即拒绝，并将拒绝第一个拒绝消息/错误。”*

**例子**

让我们写几个例子来复习如何使用`Promise.all`

在这一点上，我想你已经知道如何实现它，这是非常容易的，对不对？

**代码**

**有测试**

**你可以看到** `**Promise.myAll**` **和** `**Promise.all**` **做的是一样的事情。**

# 2.承诺.决心

我的朋友，谢谢你的阅读，我想邀请你继续进一步阅读。再来实现一下`Promise.resolve`。

*来自*[*MDN*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)*:*

*“Promise . resolve()方法”将给定值解析为承诺。如果该值是一个承诺，则返回该承诺；如果该值是一个 thenable，Promise.resolve()将使用它准备的两个回调来调用 then()方法；否则，返回的承诺将用值来履行。”*

**例子**

**代码**

我没想到`Promise.resolve`会这么容易。

**有测试**

# 3.承诺.拒绝

实现`Promise.reject`怎么样？

*来自*[*MDN*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)*:*

" Promise.reject()方法返回一个由于给定的原因而被拒绝的 Promise 对象。"

**示例**

**代码**

实现一个`Promise.reject`非常容易。我们所要做的就是确保我们返回一个新的承诺，并将结果状态设置为 reject。

**有测试**

# 4.承诺.比赛

*来自*[*MDN*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)*:*

" Promise.race()方法返回一个承诺，只要 iterable 中的一个承诺满足或拒绝，该承诺就会满足或拒绝，并返回该承诺的值或原因。"

**示例**

**代码**

你必须知道如何实现它。只要知道哪个实例先发生了变化，那么`Promise.race`就跟随着这个结果，就可以编写下面的代码了:

**有测试**

# 5.承诺。都解决了

这是我们将要实现的 Promise 的最后一个 API，实际上我们很少使用它。

以下来自 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled) :

*" promise . all settled()方法返回一个在所有给定承诺完成或被拒绝后完成的承诺，并带有一个对象数组，每个对象描述每个承诺的结果。*

当你有多个彼此不依赖的异步任务要成功完成时，或者你总是想知道每个承诺的结果时，通常会用到它。

*相比之下，如果任务相互依赖/如果你想在任何一个任务拒绝后立即拒绝，那么由 Promise.all()返回的承诺可能更合适。*

**示例**

**代号**

请坚持住，亲爱的朋友，这篇文章就要结束了。

通过上面的例子，我们总结出它的规律。

1.  无论承诺是完全成功还是部分失败，最终都会进入。然后回调`Promise.allSettled`
2.  在最终返回值中，成功和失败的项目都有 status 属性，成功时该值被满足，失败时被拒绝
3.  在最终返回值中，成功包含值属性，而失败是原因属性

**有测试**

# 最后

**感谢阅读。**我期待着您的关注和阅读更多高质量的文章。

[](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/20-javascript-array-methods-every-developer-should-know-6c04cc7a557d) [## 每个开发人员都应该知道的 20 种 JavaScript 数组方法

### 你知道这 20 个数组方法是怎么实现的吗？

javascript.plainenglish.io](/20-javascript-array-methods-every-developer-should-know-6c04cc7a557d) [](/8-cool-github-tricks-to-make-you-look-like-a-senior-developer-ab8fe9ae9b14) [## 让你看起来像高级开发人员的 8 个很酷的 GitHub 技巧

### 使用 GitHub 可以做的 8 件很酷的事情

javascript.plainenglish.io](/8-cool-github-tricks-to-make-you-look-like-a-senior-developer-ab8fe9ae9b14) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) [## 现在是 2022 年，不要再滥用箭头功能了

### 不应该使用箭头函数的 4 种情况。

javascript.plainenglish.io](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***