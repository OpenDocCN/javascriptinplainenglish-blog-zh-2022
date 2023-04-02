# 90%的人无法解决这个脸书面试问题

> 原文：<https://javascript.plainenglish.io/90-of-you-will-fail-to-answer-solve-this-facebook-interview-question-part-1-282b93e535e1?source=collection_archive---------1----------------------->

在网上做了大量研究后，我得出结论，没有专门为前端开发人员准备 MAANG (Meta，Apple，Amazon，网飞，Google)的教程/视频系列。

所以，我决定在我的 [YouTube 频道](https://www.youtube.com/results?search_query=uncommon+geeks)上解码 MAANG 最常见的面试问题。在这篇文章中，我将讨论一个非常有趣的问题。所以，继续读下去，直到结束。

![](img/d370497dc005cf03097b6c9b426c7800.png)

Facebook interview question solved

> **问题**
> 
> 将两个字符串形式的非常大的数字相加，并以字符串形式返回结果。

**提问的公司****:脸书/梅塔**

例如:

**样本输入:**

“99999999999999999999999999999” + “1”

**样本输出**

“100000000000000000000000"

**常规方法**

大多数人会认为这是一个简单的问题，可以用下面的代码片段解决。

```
function addNumbers(num1, num2){
return Number(num1) + Number(num2)
}
console.log(addNumbers("99999999999999999999999999999", "1"))
```

不幸的是，这种解决方案行不通。如果运行上面的代码，输出将是这样的: **1e+29。**

万一这是你第一次看到这种表情，那么面试的时候你的信心就少了一半。让我来帮你解释这意味着什么。

1e+29 **代表 10 ⁹ (1 * 10 的 29 次方)。**上面两个数相加，哪个其实是正确答案。但是采访者期望输出为 **100000000000000000000。**

有两种主要的方法来实现这个解决方案，我将在这一部分讨论一个解决方案，在另一部分讨论下一个解决方案。

**解决方案 1:** 使用 **BigInt**

> **BigInt** 的定义
> 
> " bigint 是一个原始的包装对象，用于表示和操作原始的 BigInt 值，这些值太大了，无法用 number 原语来表示。"

这个定义说明了一切:当一个数由于其长度较大而不能以数字的形式表示时，我们可以使用 BigInt 作为替代。

> **带解决方案的代码片段**

```
function addNumbers(num1, num2){
return BigInt(num1) + BigInt(num2)
}
console.log(addNumbers(“99999999999999999999999999999”, “1”))
```

输出将是:**100000000000000000000000000n**

这里末尾的“n”指的是一个 BigInt。

但是面试官不会期望你写出这个解决方案，因为你在用一种固有的方法来解决问题。相反，他们希望你能自己解决这个问题。这将在本文的第二部分讨论，请务必阅读。

感谢您在下一篇文章中阅读 catch you。如果你还没有在媒体上关注我，那么请关注我，你可以在链接的[这里](https://www.linkedin.com/in/vasanth-bhat-4180909b/)上关注我。别忘了订阅我的 Youtube 频道[。](https://www.youtube.com/channel/UCSCNvSCk_Z9mBvUM-FJexRg/videos)

如果你想亲自和我讨论模拟面试，面试或简历审核的技巧和诀窍，你可以在这里预约:

[](https://topmate.io/vasanth_bhat) [## 在 topmate.io 上预订与瓦桑特的时间

### 为世界顶尖人才简化个性化互动

topmate.io](https://topmate.io/vasanth_bhat) 

如果你正在准备前端开发者面试，请观看我的以下系列:

如果你想学习内置方法的 JavaScript 自定义实现，那就看看我下面的系列吧:

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*