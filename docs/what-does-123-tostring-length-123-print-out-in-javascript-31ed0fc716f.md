# 123['toString']。length + 123)用 JavaScript 打印出来？

> 原文：<https://javascript.plainenglish.io/what-does-123-tostring-length-123-print-out-in-javascript-31ed0fc716f?source=collection_archive---------1----------------------->

## 95%的前端开发者回答错误的问题。

![](img/a4b872adc770dc6d40e5560947bd73f8.png)

Photo by [Mikhail Vasilyev](https://unsplash.com/@miklevasilyev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

前一段时间，我被问到一个简单的面试问题，但我没有给出正确的答案，在开始，甚至 95%的前端开发人员都无法准确回答。面试问题是什么？让我们看一看…

一开始我以为答案是`126(3 + 123)`，但是我错了。真正的答案是什么？让我们一步步揭开谜底。

# 函数的形参数量

这很容易。所有前端开发者都知道答案。

`function`的参数与其长度一样多。但事实真的是这样吗？跟着我，继续往下看...

# 默认参数

这让我很震惊，甚至看起来和上面的答案有些不同。是的，我们可以从这里得出一个结论:

`*function.length*` *是第一个带默认值的参数前的个数。*

# 该函数的其余参数

如果一个函数有剩余的参数，如何计算“function.length”？

是的，我肯定你是对的。答案是`1`。所以我们可以得出另一个结论:

*其余参数不包括在“function.length”的计算中。*

# 摘要

最后，你知道这个问题的答案吗？

看一下 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length) 上的摘要

*长度是函数对象的一个属性，表示函数需要多少个自变量，即形参的数量。*

*该数字不包括其余参数，仅包括第一个参数之前的参数，并具有默认值。*

*相反，* `*arguments.length*` *是函数的局部变量，提供实际传递给函数的参数个数。*

# 最后

**感谢阅读。**我期待着您的关注和阅读更多高质量的文章。

[](/interviewer-can-a-1-a-2-a-3-ever-evaluate-to-true-in-javascript-d2329e693cde) [## 记者:在 JavaScript 中(a==1 && a==2 && a==3)能计算为真吗？

### 是的，这可能是真的，而且有 6 种方式——太神奇了！

javascript.plainenglish.io](/interviewer-can-a-1-a-2-a-3-ever-evaluate-to-true-in-javascript-d2329e693cde) [](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [## “我失去了一个工作机会，只是因为承诺。所有”

### 一次让我好难过的面试经历。

javascript.plainenglish.io](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) [## 现在是 2022 年，不要再滥用箭头功能了

### 不应该使用箭头函数的 4 种情况。

javascript.plainenglish.io](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***