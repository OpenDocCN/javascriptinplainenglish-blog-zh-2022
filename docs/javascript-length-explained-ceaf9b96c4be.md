# JavaScript。解释的长度

> 原文：<https://javascript.plainenglish.io/javascript-length-explained-ceaf9b96c4be?source=collection_archive---------21----------------------->

求一个字符串的长度—文章+视频+可视白板示例(我手写)

![](img/abac7261b902d67d8b0cffea6a2fd03e.png)

image credit: by author designed with canva.com

在本文中，我将向您展示如何使用 JavaScript 中的`.length`属性来查找/计算一个`String`中有多少个字符

> 目录

1.  JavaScript `.length`属性(代码编辑器示例)
2.  我们作为人类的计数方式(对此的解释在视频中)
3.  计算机计数的方式(视频中有解释)

# JavaScript。长度-查找字符串的长度

在 JavaScript 中，您可以通过在字符串变量或字符串文字后面写`.length`来找到`String`值的长度。

但实例胜于千言万语。让我们看看它的代码:

```
const **firstName** = "**Ada**";
const *myData* = **firstName.length**;console.log(*myData*);
```

代码解释:

在上面的代码中，我们有两个变量:

1.  **名字**，它保存了**“Ada”**的值

```
const **firstName** = "**Ada**";
```

2. **myData** 变量，保存 **firstName = "Ada"** 的值

还有**。变量末尾的长度**如下:firstName.length

这里我们用了**。**字符串变量后的长度**。**

。length 返回一个整数(整数)。字符数。例如:在单词“Ada”中有 3 个字符/字母。

```
const *myData* = **firstName.length**;
console.log(myData);
```

> 空字符串的`length`属性为 0。
> 
> 注意:在视频中我使用了 **var 关键字**，因为这是我 ES5 课程的一部分。

*更多内容看* [*说白了就是*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家的写作机会和建议。*