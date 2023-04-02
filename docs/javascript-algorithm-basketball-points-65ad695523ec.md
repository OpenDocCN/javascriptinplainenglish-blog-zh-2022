# JavaScript 算法:篮球积分

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-basketball-points-65ad695523ec?source=collection_archive---------5----------------------->

## 计算篮球比赛中的得分

![](img/88972874718adbce2a07a64a4758abed.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`points`的程序，它将接受两个整数`two_point`和`three_point`。

你正在计算一场篮球赛的总得分。在这些分数范围内，会给出两分球得分的数量和三分球得分的数量。该函数的目标是输出团队的总分数。

示例:

```
points(7,5) // 29
```

对于上面的例子，2 分球的数量是`7`，3 分球的数量是`5`。

乘以`7 * 2`得到 14。

乘`5 * 3`等于 15。

把`14 + 15`加在一起就是`29`。

该功能简短而简单。首先，我们创建两个变量:

```
two_point
three_point
```

`two_point`变量代表两分球得分的数量。`three_point`变量代表三分球得分的多少。

知道了这一点，我们用`2`乘以 2 分球的数量，用`3`乘以 3 分球的数量。

```
two_point * 2
three_point * 3
```

我们将两个方程相加，然后返回:

```
return two_point*2 + three_point*3;
```

您还可以将总数赋给一个名为`total`的变量或其他变量，并返回该变量。

```
let total = return two_point*2 + three_point*3;
return total;
```

不管怎样，就是这样。下面是完整的函数:

如果您觉得这个算法有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](/javascript-algorithm-chessboard-889d01612fe5) [## JavaScript 算法:棋盘

### 创建 8×8 网格棋盘

javascript.plainenglish.io](/javascript-algorithm-chessboard-889d01612fe5) [](https://endubueze00.medium.com/javascript-algorithm-looping-a-triangle-b31c62044efd) [## JavaScript 算法:循环三角形

### 创建半个三角形

endubueze00.medium.com](https://endubueze00.medium.com/javascript-algorithm-looping-a-triangle-b31c62044efd) [](/javascript-algorithm-creating-a-multiplication-chart-22ef49a7a29) [## JavaScript 算法:创建乘法表

### 如何用 JavaScript 创建简单的乘法表

javascript.plainenglish.io](/javascript-algorithm-creating-a-multiplication-chart-22ef49a7a29) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*