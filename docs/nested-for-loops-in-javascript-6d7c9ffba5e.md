# JavaScript 中嵌套的“for”循环

> 原文：<https://javascript.plainenglish.io/nested-for-loops-in-javascript-6d7c9ffba5e?source=collection_archive---------4----------------------->

## 关于如何在 JavaScript 中使用嵌套“for”循环的教程

![](img/f29cd0cde116af445de3cca608d0061c.png)

## 介绍

我以前发表过一篇关于 JavaScript 中 for 循环的文章，可以在这里访问[。为了完整起见，我将简单地给出一个 JavaScript 中 For 循环的例子。](https://blog.devgenius.io/the-anatomy-of-a-for-loop-in-javascript-9523c3da0d59)

```
const arr = [1, 2, 3, 4, 5, 6];for(let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}//Returns --->1
2
3
4
5
6
```

*   在上面的例子中，我们首先声明一个名为 *arr* 的变量，并给它分配一个包含数字 1 到 6 的数组。
*   接下来，我们创建一个 for 循环，我们初始化一个名为 *i* 的变量，它作为循环的计数器。
*   接下来，我们使用一个条件来决定何时循环应该停止运行。在我们的例子中，当 *i* 小于 *arr* 数组的长度时，我们将继续运行循环。
*   最后，对于更新程序，我们说每次循环运行时，我们应该增加 *i* 。
*   在循环体内部，我们使用控制台日志打印出循环运行时位于 *i* 索引处的 *ar* r 数组的元素。

这样做的结果是 *arr* 数组中的每个元素都被打印出来。

有时，您可能会发现自己面对的是更复杂的数据结构，比如嵌套数组。让我们先来看看当我们对这种类型的数据结构使用上面的循环时会发生什么。

```
const arr = [[1, 2], [3, 4], [5, 6]];for(let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}//Returns ---> 
[1, 2]
[3, 4]
[5, 6]
```

在上面的例子中，我们使用了相同的 for 循环，但是这次, *arr* 数组包含三个嵌套数组，每个嵌套数组包含两个值。当循环运行时，我们返回每个嵌套数组。如果我们想访问嵌套数组的单个元素呢？这就是嵌套 for 循环有用的地方。

## 嵌套循环

通过使用嵌套循环，我们可以访问嵌套数组中的单个元素。让我们看一个例子，看看上面的例子是如何工作的。

```
const arr = [[1, 2], [3, 4], [5, 6]];for(let i = 0; i < arr.length; i++) {
  for(let j = 0; j < arr[i].length; j++) {
    console.log(arr[i][j]);
  }
}//Returns --->1
2
3
4
5
6
```

嵌套循环的结果是我们能够列出嵌套数组中的每个单独的元素。现在让我们来分析一下这是怎么回事。我们已经知道外部循环访问每个嵌套数组。当这种情况发生时，内部循环遍历嵌套数组中的每个元素。所以控制台日志本质上是说对于数组元素 *i* ，也就是包含 1 和 2 的数组使用 *j* 遍历这些元素。让我们进一步分析一下。对于循环的第一次迭代，我们得到以下结果:

```
const arr = [[1, 2], [3, 4], [5, 6]];for(let i = 0; i < arr.length; i++) {
  console.log(`I am the outer loop ${arr[i]}`) for(let j = 0; j < arr[i].length; j++) {
    console.log(`I am the inner loop ${arr[i][j]}`)
  }
}//Returns --->
I am the outer loop 1,2
I am the inner loop 1
I am the inner loop 2
```

因此，外部循环返回包含元素 1 和 2 的第一个嵌套数组。然后，内部循环依次遍历嵌套数组的每个元素。因此我们得到 1 然后得到 2。

这个过程对嵌套数组的整个数组运行。因此，这些控制台日志的最终输出如下。

```
const arr = [[1, 2], [3, 4], [5, 6]];for(let i = 0; i < arr.length; i++) {
  console.log(`I am the outer loop ${arr[i]}`) for(let j = 0; j < arr[i].length; j++) {
    console.log(`I am the inner loop ${arr[i][j]}`)
  }
}//Returns --->
I am the outer loop 1,2
I am the inner loop 1
I am the inner loop 2I am the outer loop 3,4
I am the inner loop 3
I am the inner loop 4I am the outer loop 5,6
I am the inner loop 5
I am the inner loop 6
```

## 字符串数组

如果您有一个单词数组，并且想要遍历每个字母，这种方法同样有用。让我们看一个例子。

```
const names = ["Abby", "Bobby", "Freddy"];for(let i = 0; i < names.length; i++) {
  console.log(names[i]);
}//Returns --->
Abby
Bobby
Freddy
```

使用 for 循环，我们遍历 names 数组，我们可以访问 *names* 数组中的每个元素。这很好，但是如果你想访问名字的单个元素，那么嵌套循环是一个非常有用的模式。

```
const names = ["Abby", "Bobby", "Freddy"];for(let i = 0; i < names.length; i++) {
  console.log(`I am the outer loop ${names[i]}`) for(let j = 0; j < names[i].length; j++) {
    console.log(`I am the inner loop ${names[i][j]}`)
  }
}//Returns --->
I am the outer loop AbbyI am the inner loop A
I am the inner loop b
I am the inner loop b
I am the inner loop yI am the outer loop BobbyI am the inner loop B
I am the inner loop o
I am the inner loop b
I am the inner loop b
I am the inner loop yI am the outer loop Freddy
I am the inner loop r
I am the inner loop e
I am the inner loop d
I am the inner loop d
I am the inner loop y
```

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****