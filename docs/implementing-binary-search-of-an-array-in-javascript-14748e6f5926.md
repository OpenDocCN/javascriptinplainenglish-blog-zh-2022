# 用 JavaScript 实现数组的二分搜索法

> 原文：<https://javascript.plainenglish.io/implementing-binary-search-of-an-array-in-javascript-14748e6f5926?source=collection_archive---------15----------------------->

![](img/1905e2b4ff7163e15131c20536147165.png)

# **二分搜索法**

让我们从了解什么是二分搜索法开始。是一个[搜索算法](https://en.wikipedia.org/wiki/Search_algorithm)在一个排序的数组中找到一个目标值的位置。

它的工作原理是重复地将排序后的数组分成两半，直到你将可能的位置缩小到只有一个。

# 伪代码

伪代码是对计算机编程算法的描述，它使用编程语言的结构约定，但省略了特定于语言的语法。

这是二分搜索法的伪代码，修改后可以在数组中搜索。输入是数组，我们称之为`array`；`array`中元素的数量`n`；以及`target`，被搜索的号码。输出为`target`的`array`中的指标:

1.  让`min = 0`和`max = n-1`。
2.  将`guess`计算为`max`和`min`的平均值，向下舍入(使其为整数)。
3.  如果`array[guess]`等于`target`，则停止。你找到了！返回`guess`。
4.  如果猜测值过低，即`array[guess] < target`，则设置`min = guess + 1`。
5.  否则，猜测就太高了。设置`max = guess - 1`。
6.  回到步骤 2。

# **如果你要找的数字是数组中的*而不是*该怎么办？**

让我们为二分搜索法编写伪代码，处理目标号码不存在的情况:

1.  让`min = 0`和`max = n-1`。
2.  如果`max < min`，则停止:`target`不在`array`中。返回`-1`。
3.  将`guess`计算为`max`和`min`的平均值，向下取整(因此它是一个整数)。
4.  如果`array[guess]`等于`target`，则停止。你找到了！返回`guess`。
5.  如果猜测值过低，即`array[guess] < target`，则设置`min = guess + 1`。
6.  否则，猜测就太高了。设置`max = guess - 1`。
7.  回到步骤 2。

# 伪代码实现

现在让我们把伪代码变成一个 JavaScript 程序。

*   首先，让我们创建一个函数，因为我们的代码将接受输入并返回输出
*   我们也希望我们的代码对于不同的输入是可重用的
*   让我们进入函数体，并决定如何实现它。
*   第 6 步说回到第 2 步。那听起来像一个循环。应该是 for 循环还是 while 循环？
*   while 循环是更好的选择，因为二分搜索法猜测的索引不像 for 循环那样按顺序排列。
*   按照下面的伪代码完成`Search`函数，以便它实现一个二分搜索法(这个伪代码已经在上面描述过了):
    1。让`min = 0`和`max = n-1`。
    2。如果`max < min`，那么停止:目标不在数组中。返回`-1`。
    3。将`guess`计算为`max`和`min`的平均值，向下舍入(因此它是一个整数)。
    4。如果`array[guess]`等于目标，则停止。你找到了！返回`guess`。
    5。如果猜测太低，即`array[guess]`目标为`<`，则设置`min = guess + 1`。6。否则，猜测就太高了。设置`max = guess - 1`。
    7。回到步骤 2。

```
/* Returns either the index of the location in the array,
  or -1 if the array did not contain the target */
var Search = function(array, target) {
 var min = 0;
 var max = array.length - 1;
    var guess;

    while(min <= max) {
    guess = Math.floor((max + min) / 2);if (array[guess] === target) {
        return guess;
    }
    else if (array[guess] < target) {
        min = guess + 1;
    }
    else {
        max = guess - 1;
    }}return -1;
};var primes = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 
  41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97];var result = Search(primes, 73);
println("Found prime at index " + result);//Program.assertEqual(Search(primes, 73), 20);
```

## 快乐学习！

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*