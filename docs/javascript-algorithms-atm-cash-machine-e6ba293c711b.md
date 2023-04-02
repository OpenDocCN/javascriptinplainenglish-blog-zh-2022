# JavaScript 算法:ATM(取款机)

> 原文：<https://javascript.plainenglish.io/javascript-algorithms-atm-cash-machine-e6ba293c711b?source=collection_archive---------4----------------------->

![](img/0f8063373119675765a2d6f7e23fd726.png)

Photo by [Jake Allen](https://unsplash.com/@jakeallenmedia?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/atm?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在本文中，我们将考虑在面试问题中经常使用的热门任务自动柜员机。任务语句大概是这样的:
有 ***k*** 不同面额的纸币在流通: *a* 1、 *a* 2、…，以此类推。ATM 必须使用最少数量的钞票来分发该金额，或者报告不能分发所请求的金额。自动柜员机可以有或没有发行限制。

让我们考虑无限发行钞票的第一个选项，并写出我们任务的条件。

## 描述

有一台 ATM，纸币面额 ***100，50，20，10，5*** 。纸币数量*无限*。需要发行*最少*张钞票。金额必须大于 ***零*** 并且是最小钞票的倍数

**例 1:**

```
**Input:** 375
**Output:** [100,100,100,50,20,5]
```

**例 2:**

```
**Input:** 0
**Output:** Please enter an amount greater than zero
```

**例 3:**

```
**Input:** 3
**Output:** Please enter the amount in multiples of 5
```

## 解决办法

现在，让我们的任务复杂化，增加我们的 ATM 机可用的面额。复杂的是，现在我们必须计算 ATM 中可用的金额。如果用户希望收到超过可用金额的金额或无法支付的金额，那么我们必须通知他

**例 1:**

```
**Input:** 375, {100: 5, 50: 3, 20: 20, 10: 5, 5: 1}
**Output:** [100,100,100,50,20,5]
```

**例二:**

```
**Input:** 23, {100: 5, 50: 3, 20: 20, 10: 5, 5: 1}
**Output:** Failed to issue this amount, try another amount
```

在这种情况下，我们不能发行这个数量，因为我们没有面额 3

**例 3:**

```
**Input:** 800, {100: 5, 50: 3}
**Output:** Failed to issue this amount, try another amount
```

在这种情况下，我们不能提取这笔金额，因为我们在 ATM ***中有最大可用金额 500 * 5+ 50 * 3 = 650***

## 解决办法

有时，在这个任务中，要求答案不是以数组的形式显示，而是以对象的形式显示。

**例如:**

```
**Input:** 375, {100: 5, 50: 3, 20: 20, 10: 5, 5: 1}
**Output:** {100: 3, 50: 3, 20: 1, 5: 1]
```

然后，我们需要稍微修改这段代码的函数的最后一部分

ATM 中存在非标准命名的任务，在这种情况下，此算法将无法在所有情况下正常工作。让我们看一个例子:

**举例:**

```
**Input:** 240, {100: 5, 80: 3, 20: 1}
**Output:** {80: 3]
```

如果我们尝试运行我们的函数，我们将得到“*未能发出此金额，尝试另一个金额”*。事实是，我们不检查替代选项，而只是简单地尝试按照从大额钞票到小额钞票的顺序发行金额。

为了让我们检查替代选项，如果第一次搜索没有找到所需的金额，我们将需要递归调用从面额中查找金额的函数。

让我们看看它会是什么样子

嗯，你可能需要的最后一件事是在错误中显示一个提示，这是发行的最小可用面额和最大可用金额，让我们将所有这些合并到一个通用函数中。

希望对你有用！

感谢阅读！回头见。😊

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****