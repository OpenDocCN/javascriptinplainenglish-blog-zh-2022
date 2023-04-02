# 让你成为更好的程序员的 5 个必须知道的 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/5-must-know-javascript-tricks-tips-to-make-you-a-better-programmer-a3d56a688ad3?source=collection_archive---------0----------------------->

## 如果你想成为一名更好的程序员，请一定要学会这些技巧。

![](img/13bff9f747622ce341d6cee7ead7c25f.png)

Photo by [Jari Hytönen](https://unsplash.com/@jarispics?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们每天都要写条件语句，它是程序代码中非常重要的一部分。

有没有想过优化条件语句？

**本文将与你分享做到这一点的 5 个技巧，希望你会喜欢！**

# 1.请使用“[”。包括"而不是" || "

这段代码看起来很简单，因为我们只检查了两个名字。

但是需要查的名字多了怎么办？

也许我们可以继续使用“||”来扩展判断，但是相信我，这不是一个好主意。

我们的代码将变得更加难以维护，它将变得肮脏。

其实只要使用数组的`includes`方法就可以完美解决这个问题。

如果需要对同一个变量进行多次判断，可以使用数组的 includes()方法进行优化，该方法可用于判断数组中是否存在指定的元素，如果指定的元素存在，则返回`true`，如果不存在，则返回`false`。

# 2.请不要吝啬“]。每一个“和”]。一些”

朋友们，我相信我们都曾经写过这样的代码片段。确定数组中的所有元素是否满足指定的条件。

但是 JavaScript 中的数组提供了`every()`方法，用于检查数组中的所有元素是否满足给定的条件。当每个数组元素满足给定条件时返回`true`，否则返回`false`。

我们可以用它来优化上面的代码。

哇！我们设法只用一行代码做了所有的事情！！！太棒了。

当然啦！如果你只想检查数组中是否至少有一个元素匹配指定的条件，我们可以使用数组的`some`方法。

# 3.#不要写太多“如果…。否则”。

有什么方法可以优化这段代码吗？

是的，我们有办法让它在输入无效的情况下提前返回`fruit`。

其实还可以进一步优化，如果`blueFruits`不含`fruit`，可以更早结束

# 4.#默认参数是天使

我们经常需要对传递给函数的参数做一些事情，比如没有传入价格时的默认值$10。

我们实际上可以用默认参数优化上面的代码。

# 5.#请使用“&&”运算符来简化代码

对于逻辑 AND 运算符，如果左边的条件为假，则直接发生短路，执行无法继续；

如果左边的条件为真，则返回右边的计算结果。所以，对于这个 if 中只有一行表达式的情况，可以用逻辑 AND 运算符来简化，其中左边是判断条件，右边是要执行的逻辑:

# 最后

**感谢阅读。**我期待期待您的关注和阅读更多高质量的文章。

[](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [## “我失去了一个工作机会，只是因为承诺。所有”

### 一次让我好难过的面试经历。

javascript.plainenglish.io](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) [## 现在是 2022 年，不要再滥用箭头功能了

### 不应该使用箭头函数的 4 种情况。

javascript.plainenglish.io](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*