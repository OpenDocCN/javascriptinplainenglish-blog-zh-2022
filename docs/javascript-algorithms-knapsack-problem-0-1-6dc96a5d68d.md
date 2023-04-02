# JavaScript 算法:背包问题(0–1)

> 原文：<https://javascript.plainenglish.io/javascript-algorithms-knapsack-problem-0-1-6dc96a5d68d?source=collection_archive---------0----------------------->

![](img/5cd74b978bd83ccc7fc34228cb55ff4d.png)

Photo by [Denisse Leon](https://unsplash.com/@denisseleon?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/knapsack?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

背包问题是组合优化中的一个问题:给定一组项目，每个项目都有一个重量和一个值，确定要包含在集合中的每个项目的数量，使得总重量小于或等于给定的限制，并且总值尽可能大。它的名字来源于一个人所面临的问题，他被一个固定大小的背包所限制，必须用最有价值的物品装满它。

在本文中，我们将分析一些解决这一问题的方法。

## 描述

给定背包 ***的容量 W = 40，*** 物品列表 ***的值=【10，20，30，40】***， ***的权重=【30，10，40，20】***

**例 1:**

```
**Input:** w = 40, values = [10,20,30,40], weights = [30,10,40,20]
**Output:** 60
```

## 解决办法

解决这个问题有几种选择:

## ***强力递归***

递归将创建总重量小于给定容量 w 的项目的所有子集。根据结果，我们将返回具有最大值的子集。

## 动态编程(记忆化)

在这种方法中，我们将把所有计算出的答案存储在 *hashMap* 中，关键元素索引在行中，权重在列中，并在以后用于重叠的子任务。仍将使用递归传递。

## 动态规划(迭代)

我们创建一个由`n + 1`行和`w + 1`列( *w —容量*)组成的二维数组(即表格)。行号 *i* 表示第 1 — *i* 行中所有项目的集合。例如，第 3 行中的值假设我们只有项目 1、2 和 3。

将所有东西放在一起，行 *i* 列 *j* 中的一个条目表示在一个可以容纳 *j* 重量单位的背包中，用物品 1、2、3……*I*可以获得的最大值。

一旦表格被填充，最终的解决方案可以在最后一列的最后一行中找到，这代表了用*所有物品*和背包的*满容量*可获得的最大值。

该算法可以表示如下:

希望对你有用！

感谢阅读！回头见。😊

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***