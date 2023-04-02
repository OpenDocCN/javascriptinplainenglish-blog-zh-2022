# JavaScript For 循环条件表达式

> 原文：<https://javascript.plainenglish.io/javascript-for-loop-condition-expression-2347bf9624a8?source=collection_archive---------3----------------------->

![](img/4481351bddc6bbb4757d82afe1ec14a0.png)

Photo by [Lysander Yuen](https://unsplash.com/@lysanderyuen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都知道 JavaScript 中什么是 for 循环:

```
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

如果你运行上面的代码，它会打印出五个数字。尽管我们每天都在使用它，我想我们并没有真正注意到定义的第二部分实际上是一个条件表达式，`i < 5`。

> 对`conditionExpression`表达式进行评估。如果`conditionExpression`的值为真，则执行循环语句。否则，`for`循环终止。

根据文档记载，[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Guide/Loops _ and _ iteration # for _ statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration#for_statement)，`i < n`其实就是一个表达式。此外，它是一个表达式，在每次迭代之前都会被求值。

## 更改限制

让我们试一试:

```
let n = 5;for (let i = 0; i < n; i++) {
  n = 6;
  console.log(i);
}
```

你猜怎么着，你又多了一份打印件`0,1,2,3,4,5`。

哇，这不是糟糕的代码吗？我可以想象 10 个人中有 9 个人会第一眼就称之为糟糕的代码，然而，我在一些严肃的库源代码中见过这种用法。

你可能会问，这有什么用？假设我们在一个数组中有一个作业 id 列表:

```
const v = [2, 1, 3]; for (let i = 0; i < v.length; i++) {
  if (v[i] === 1) v.push(4)
  console.log(v[i])
}
```

在处理该列表的过程中，如果我们看到 id 为`1`的作业，我们会将 id 为`4`的作业追加到列表中。

在我们的例子中，输出结果是`2,1,3,4`。此时你可能会想，既然数组在扩展，我们会进入无穷大吗？这是可能的，但只是因为你设计了支持它的逻辑。

## 不同的表达

现在，出于我们的好奇，我们能不能换一个完全不同的表达方式来代替`i < n`。我相信我们可以:

```
let done = false;for (let i = 0; (!done) && i < 5; i++) {
  done = true
  console.log(i)
}
```

让我们猜测一下从上面的例子中我们得到了多少打印输出。是的，你猜对了，我们得到的是`0`而不是`0,1,2,3,4`。所以本质上，你可以看到 for 循环和 while 循环没什么不同。语法不同，但行为即使不完全相同，也非常相似。可能用`for`的语法更紧凑！

在每次迭代中，在 for 循环之外定义的变量可能会发生任何事情。如果改变影响了表达式，那么你将得到一个有趣的循环:)

## 摘要

JavaScript for-loop 非常类似于 while-loop，其中终止循环的条件是基于表达式的，该表达式可以基于前面定义的任何变量。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****