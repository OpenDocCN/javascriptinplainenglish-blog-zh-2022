# 如何用简单的 JavaScript 求解动态规划算法

> 原文：<https://javascript.plainenglish.io/how-to-solve-dynamic-programming-algorithms-with-simple-javascript-ddeb0e5dd68e?source=collection_archive---------9----------------------->

## 编码能力很重要

![](img/fbe59f2721925699da6dab3dd6abd6fa.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

动态规划是算法面试中非常常见的题目类型。但他们的解决方案是有迹可循的。它可以分为以下四个步骤:

**1。确定 DP 数组下标的含义。**

**2。确定递归公式。**

**3。确定 DP 阵列的初始化值。**

**4。确定 DP 数组的遍历顺序。**

请记住上面的四个步骤，我们会按照这四个步骤来分析每一个动态规划问题，开始吧！

# [1。斐波那契数](https://leetcode.com/problems/fibonacci-number/)

分析如下:

1.  确定 DP 数组下标的含义:这里`dp[i]`代表第 I 项对应的值
2.  确定递归公式:题目中已经给出，转换成代码是`dp[i] = dp[i - 1] + dp[i - 2]`
3.  确定 DP 数组初始化值:已经在标题中给出，`dp[0] = 0`和`dp[1] = 1`
4.  确定遍历顺序:因为我们寻求 dp[n]，所以我们从左向右遍历

# [2。独特的路径](https://leetcode.com/problems/unique-paths/)

分析如下:

1.  确定 DP 数组下标的含义:`dp[i][j]`表示从坐标`(0, 0)`开始到坐标`(i, j)`有`dp[i][j]`条不同的路径
2.  确定递推公式:要到达坐标`(i, j)`，只能从`(i-1, j)`或`(i, j - 1)`出发，所以`dp[i][j ] = dp[i - 1][j] + dp[i][j - 1]`
3.  确定 DP 数组的初始化值:从坐标`(0, 0)`开始，到达水平和垂直方向的起始坐标路径只有一条，所以我们需要使用一个循环。`for (let i = 0; i < m; i += 1) dp[i][0] = 1`和`for (let i = 0; i < n; i += 1) dp[0][ i] = 1`
4.  确定遍历顺序:因为我们寻找`dp[m - 1][n - 1]`，所以我们从左向右遍历

# [3。独特路径二](https://leetcode.com/problems/unique-paths-ii/)

分析如下:

1.  确定 DP 数组下标的含义:`dp[i][j]`表示从坐标`(0, 0)`出发，到达坐标`(i, j)`有`dp[i][j]`条不同的路径
2.  确定递归公式:由于这个问题中有障碍点，如果要到达坐标`(i, j)`，需要判断`(i, j)`是否是障碍点，如果没有路径可以到达，那么`dp[i][j] = 0`，如果没有，需要经过`(i-1, j)`或者`(i, j - 1)`，然后`dp[i][j] = dp [i - 1][j] + dp[i][j - 1]`
3.  确定 DP 数组的初始化值:从坐标`(0, 0)`开始，到达水平和垂直方向的起始坐标路径只有一条，所以我们需要使用一个循环。但是你在循环中需要小心，一旦遇到障碍物就需要退出循环，因为机器人无法到达后面的点。
4.  确定遍历顺序:因为我们寻找`dp[m - 1][n - 1]`，所以我们从左向右遍历

感谢阅读！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和谐***](https://discord.gg/GtDtUAvyhW) ***。******