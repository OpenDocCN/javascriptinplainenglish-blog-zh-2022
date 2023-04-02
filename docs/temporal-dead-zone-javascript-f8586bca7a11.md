# 面向初学者的 JavaScript 时间死区介绍

> 原文：<https://javascript.plainenglish.io/temporal-dead-zone-javascript-f8586bca7a11?source=collection_archive---------16----------------------->

## 关于时间死区的初学者教程。

![](img/02fbadeeb5a2d07f0afd1b1c2cb87a11.png)

Photo by [Andy Li](https://unsplash.com/@andylid0?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

时间死区是 JavaScript 中最直白的术语，但人们通常不太理解它。今天就试着解码一下吧。

首先，让我们把这个术语分成两部分:
暂时的——只持续一段时间
暂时的死亡——在一定时间内死亡的人
暂时的死亡地带——某物死亡的地带或区域。(我们很快就会知道这是什么。)

现在，在你从椅子上跳起来思考之前，我们指的是僵尸或一些恐怖电影。让我搞清楚，这个术语直接来自 ES6。

问题是这个区域到底是什么，在它之外会有什么样的生活。嗯，有意思！

让我们从做一些练习开始:

```
console.log(a); // 1
var a = 5;
```

这里第 1 行的输出是什么，现在根据 JavaScript 的提升概念，上面的行被重写为:

```
var a;
console.log(a); // Answer is undefined
a = 5;
```

现在，对 ES6、const 和 let 中的一些新声明类型进行相同的操作。

```
console.log(c); // 1
const c= 5;
```

这里的输出会是什么？

```
Not undefined , but a deadly red error - Uncaught ReferenceError: c is not defined
    at <anonymous>:1:13 , Why because our dear c variable is dead and is not live yet
```

下面的片段也是如此:

```
console.log(d);
let d = 5;
```

那么，为什么会出现这种错误，时间死区又是如何适应这里的呢？

因为 let 和 const 是块范围变量，从块开始的点到 let/const 点被定义，这个点被称为这些变量的时间死区。为什么？因为，与 var 不同，const 和 let 没有被提升，因此，在它们被定义之前，它们实际上是死的或不存在的。因此，对于我们的块范围变量，该区域被称为 TDZ。如果你试图在 TDZ 访问这个变量，你会得到如上的引用错误。

为了形象地说明这一点，下面是 TDZ 的定义:

```
{
 var a = 10 ;      // Temporal Dead Zone for b and c
 console.log(a);   // Temporal Dead Zone for b and c
 console.log(b);   // Temporal Dead Zone for b and c
 let b = 5;        // Temporal   Dead Zone for c
 console.log(c);  // Temporal Dead Zone for c
 const c = 5;      // No Temporal dead zone
}
```

简而言之，这就是时间死区。希望你现在明白了😃，TDZ 到底是什么，能够更好地向别人解释。🙌如果你有任何疑问或建议，请在评论区告诉我。

关于我——我是一个编程爱好者，喜欢阅读和写作前端设计、JavaScript、UI/UX 相关的东西。点击[这里](https://medium.com/@avinash.dev21987)阅读我的所有文章。

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。**