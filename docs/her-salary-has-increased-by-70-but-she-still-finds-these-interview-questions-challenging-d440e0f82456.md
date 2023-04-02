# 帮我获得阿里巴巴录用的前端面试。

> 原文：<https://javascript.plainenglish.io/her-salary-has-increased-by-70-but-she-still-finds-these-interview-questions-challenging-d440e0f82456?source=collection_archive---------4----------------------->

一个优秀的女孩。

![](img/b776ba7b7ab8a7358caebc1ddb7f854c.png)

# 前言

最近，我的好朋友正在换工作，并在网上收到了许多邀请。尽管她的薪水增加了 70%，她还是觉得这些面试问题很有挑战性。让我们来看看。

# 1.查找两个节点中最近的公共父节点，包括节点本身

**简介:**

oNode1 和 oNode2 在同一个文档中，不会是同一个节点。

```
function findCommonParent(oNode1, oNode2) {
  *// fill here*
}
```

我相信你看到这个问题会用递归，但是没有明确的思路。

这个时候不要紧张。从问题中找出更多有效信息，尽量多用笔画(如果是现场面试，记得只带铅笔，有时候画多了思路就出来了)。

# 1.1 两个节点处于同一级别

让我们试着画出这两个节点之间可能的关系。如下图所示，它们的直接父节点就是答案。

![](img/a95f8acb4e75e9ae1e48168284ed8c24.png)

# 1.2 Rwo 节点是彼此的祖先

oNode1 是目标节点。当然反过来也是一样的。oNode2 也可以是 oNode1 的祖先。

![](img/b52558702fdbe50613d664aa86081013.png)

# 1.3 两个节点之间没有关系

如下图所示，两个节点的距离很远，看似没有关系，但如果从其中任何一个向上搜索，肯定能找到包含 oNode1 或 oNode2 的点。

![](img/5d70f41db416c483254b1866f74f967b.png)

# 1.4 递归实现版本

根据上面的分析，相信你很快就能写出下面的代码。

# 1.5 遍历实现版本

递归很好理解，仅仅通过遍历就可以实现吗？事实上，递归问题往往可以通过遍历来解决。

# 2.设计一个可以设置截止日期的本地存储 API

localstorage 不会像 cookies 一样自动过期，所以过期时间需要自己维护。

我的思路是:

使用 setItem 时，保存到期时间。使用 getItem 时，将时间与当前时间进行比较，如果大于当前时间，则返回值即可，否则需要通过 removeItem 移除该值并返回 null。

**有测试**

基本上符合问题的要求。当然也可以处理异常，比如空间满了，设置错了等等。

# 3.尝试实现 Promise.all API

Promise.all()方法将承诺的 iterable 作为输入，并返回一个承诺，该承诺解析为输入承诺的结果数组。

当输入的所有承诺都已解析时，或者如果输入 iterable 不包含承诺，则返回的承诺将被解析。

它会在任何输入承诺拒绝或未承诺抛出错误时立即拒绝，并将拒绝第一个拒绝消息/错误。

# 自己实现一个

**有测试**

# 4.使用 reduce 实现映射功能

这个问题会比较简单，我们直接写代码吧

```
Input: [1, 2, 3]
Output: [2, 4, 6]
```

![](img/6d5db11bd19b89dae893a82f3278e222.png)

# 5.最后

面试问题到此为止，感谢阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*