# 数据结构和算法:重复值

> 原文：<https://javascript.plainenglish.io/data-structures-and-algorithms-duplicate-values-f14d5a446785?source=collection_archive---------3----------------------->

## 如何有效地解决一个常见的面试问题

![](img/962050685d1e0914ce9b782a1d11e08f.png)

Photo by [Joshua Reddekopp](https://unsplash.com/@joshuaryanphoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一些代码面试问题不仅仅是寻找解决方案。有时会提出一个简单的问题，看看一个人是否能以最有效的方式解决这个问题。其中一个问题是重复值问题。

*给定一个整数数组，找出第一个重复值。*

例如:

第一个数组有两个重复值，`2`和`3`，但是我们想找到第一个重复值。重复值位于索引位置 5 和 6，因此返回位置 5 的值`3`。如果在数组中没有发现重复，那么返回`null`。

看着这个问题，一个人解决它的第一本能可能会涉及 for 循环。

这种暴力方法当然有效，而且得出这个解决方案并不困难。问题是它一点也不高效。数组中的每一项都需要循环两次。因此，更长的数组需要更多的循环，因此需要更多的时间来计算结果。如果我们能在没有任何嵌套循环的情况下最多遍历一次数组来找到答案，那就快多了。

有多种方法可以解决这个问题，但有一种解决方案利用了许多面试官正在寻找的算法中的一个重要概念。这个计算机科学概念被称为[哈希图](https://en.wikipedia.org/wiki/Hash_table)。JavaScript 在技术上没有自己的散列映射数据结构，但是使用对象映射键/值对可以实现非常类似的东西。

有了这些知识，我们能做的就是创建一个对象，然后遍历数组并将每个索引分配给对象中的一个键。这个值我们可以设置为`true`，表示这个数字已经被检查过了。

利用这个概念，我们可以遍历数组并检查当前索引处的数字是否已经作为一个键存在于对象中。如果是，我们将返回该数字，如果不是，我们将把它作为一个键添加，并继续到数组中的下一个索引。

马上我们就可以看到这里的代码更加简洁易读。结果与使用嵌套的 for 循环相同，但具有更高的效率，因为它最多只遍历数组一次。散列图是计算机科学中需要学习的一个重要概念，也是解决许多不同算法问题的有用的 T2。

面试官有时会问一些简单的问题，看看一个人是否理解了不仅仅是一种暴力方法，并考虑到了更高级的概念和时间复杂性。重复价值观问题就是一个很好的例子，因为它提供了一个很好的机会来展示你所知道的，并向雇主传达你有合适的东西。看看其他可以用这种方法解决的算法问题，让下一次面试变得精彩起来！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*