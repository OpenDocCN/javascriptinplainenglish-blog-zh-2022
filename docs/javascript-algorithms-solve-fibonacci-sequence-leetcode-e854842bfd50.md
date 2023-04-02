# JavaScript 算法:求解斐波那契数列(LeetCode)

> 原文：<https://javascript.plainenglish.io/javascript-algorithms-solve-fibonacci-sequence-leetcode-e854842bfd50?source=collection_archive---------2----------------------->

![](img/16d5855feb125c323f9bdf084def2032.png)

Photo by [Ludde Lorentz](https://unsplash.com/@luddelorentz?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/fibonacci?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

通常表示为`F(n)`的**斐波纳契数列**形成了一个序列，称为**斐波纳契数列**，这样，从`0`和`1`开始，每个数字都是前两个数字的和。以下整数序列中的数字 0，1，1，2，3，5，8，13，21，34，55，89，…..

即

```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

给定`n`，计算`F(n)`。

**例 1:**

```
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

**例 2:**

```
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

**例 3:**

```
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

**约束:**

*   `0 <= n <= 30`

## 解决办法

解决这个问题有几种选择:*递归方法、优化递归方法、迭代方法、优化迭代方法、矩阵求幂方法、数学方法*。

## **递归方法**

一种简单的方法是直接递归实现数学递推关系。解决这个问题最慢的方法因为需要指数级的*时间复杂度*:***o(2^n)****空间复杂度* : ***O(N)*** 。

## 递归**使用记忆(自顶向下方法)**

我们可以通过存储到目前为止计算的斐波那契数来避免递归中的重复工作。我们只需要将所有的值存储在一个地图中。*时间复杂度* : ***O(N)*** 和*空间复杂度* : ***O(N)*** 。

## 迭代**方法**

迭代，使用已经计算的斐波纳契值，求解所有子问题并返回 N 元素的答案。*时间复杂度* : ***O(N)*** 和*空间复杂度* : ***O(N)*** 。

## 迭代方法(**空间优化)**

我们可以优化存储前两个数字的迭代方法，因为这是我们得到序列中下一个斐波纳契数所需要的。*时间复杂度* : ***O(N)*** 和*空间复杂度* : ***O(1)*** 。

## 矩阵求幂方法

使用矩阵求幂从结果矩阵中的 *(0，0)* 处的元素中得到斐波那契数。为了做到这一点，我们可以依靠斐波那契数列的矩阵方程，找到第 N 个斐波那契数:

![](img/4d67381da9b5c9c79baef5a2a6677166.png)

这个公式是如何工作的你可以看看[维基](https://en.wikipedia.org/wiki/Fibonacci_number#Matrix_form)

这个解有:*时间复杂度* : ***O(logN)*** 和*空间复杂度*:***O(logN)***。

## 数学方法

我们可以使用`golden ratio forumula`:

![](img/10084983bf21d60e40778b645c0856ce.png)

这里有一个[链接](http://demonstrations.wolfram.com/GeneralizedFibonacciSequenceAndTheGoldenRatio/)来了解更多关于斐波那契数列和黄金分割率的工作原理。

这个解有:*时间复杂度*:***O(logN)***和*空间复杂度* : ***O(1)*** 。

> 此外，有时需要返回的不是给定 N 的值，而是给定 N 之前的 Fibonacci 元素数组。

**例如:**

```
Input: n = 7
Output: [0, 1, 1, 2, 3, 5, 8, 13]
```

在这种情况下，最合适的解决方案是 ***迭代方法***
但是返回数组本身:

和 ***递归*** ***使用记忆化*** 变化不大:

我们已经考虑了解决斐波纳契问题的不同选择，最难理解的是矩阵求幂，但通常了解前面的 4 种方法就足够面试了。

希望对你有用！

感谢阅读！回头见。😊

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***