# JavaScript 算法:创建乘法表

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-creating-a-multiplication-chart-22ef49a7a29?source=collection_archive---------9----------------------->

## 如何用 JavaScript 创建简单的乘法表

![](img/79d569c632adbe247eac263bbefad945.png)

Photo by [Enric Moreu](https://unsplash.com/@enric_moreu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`multiplication()`的函数，它将接受一个整数`num`作为参数。

该函数的目标是将乘法表从 1 输出到`num`(您的输入)。在每个表中，该函数将打印出每个数字的倍数，最大为 10。该函数还将一次一行地打印出表格，类似于乘法表。

这里有一个例子:

```
multiplication(4);//output below1 2 3 4 5 6 7 8 9 10
2 4 6 8 10 12 14 16 18 20
3 6 9 12 15 18 21 24 27 30
4 8 12 16 20 24 28 32 36 40
```

在此示例中，该函数创建了 4 个乘法表，提供了从 1 到 10 的每个数字的倍数。虽然表格并不完美，也没有整齐地对齐，但该函数将每个表格打印在自己的行上。

首先，我们创建一个名为`line`的变量:

```
let line = "";
```

我们将使用这个变量来帮助我们打印出乘法表的行。

接下来，我们将创建嵌套的 for 循环。创建乘法表时，该函数需要知道图表将包含多少个表或行。这就是外部 for 循环要做的事情。

使用上面的例子，外部 for 循环将循环 4 次。对于外部循环中的每个数字，内部 For 循环将输出该表中该数字的倍数，最大为 x 乘以 10。

```
for (let x = 1; x <= num; x++) {
    for (let i = 1; i <= 10; i++) { }
}
```

在内部 for 循环中，每次乘法之后，我们将结果追加到 line 变量中。这不仅将整数转换成字符串，还格式化了表格，使数字之间有一定的间隔。

```
for (let x = 1; x <= num; x++) {
    for (let i = 1; i <= 10; i++) {
        line += x * i + " ";
    }
}
```

在内部 for 循环完成当前行之后，我们在开始下一个表之前，控制台日志`line`并重置变量。

```
for (let x = 1; x <= num; x++) {
    for (let i = 1; i <= 10; i++) {
        line += x * i + " ";
    }
    console.log(line)
    line = "";
}
```

就是这样。下面是该函数的其余部分:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-convert-string-to-camel-case-9a72da82287f) [## JavaScript 算法:将字符串转换为骆驼大小写

### 将破折号和/或下划线分隔的单词转换为骆驼大小写

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-convert-string-to-camel-case-9a72da82287f) [](/javascript-algorithm-list-filtering-5ad64fa2d264) [## JavaScript 算法:列表过滤

### 从数组中移除所有字符串

javascript.plainenglish.io](/javascript-algorithm-list-filtering-5ad64fa2d264) [](https://levelup.gitconnected.com/javascript-algorithm-reverse-words-9ddae3a3ba39) [## JavaScript 算法:反转单词

### 反转字符串中的每个单词

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-reverse-words-9ddae3a3ba39) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*