# 在 JavaScript 中引入随机数

> 原文：<https://javascript.plainenglish.io/introducing-random-numbers-in-javascript-6da81ab665ba?source=collection_archive---------15----------------------->

## 如何用 JavaScript 创建随机数的教程

![](img/ac459e814da404427f77320c72926374.png)

当我们编写代码时，有时需要完成的任务之一是创建一个随机数。JavaScript 中的 Math 对象提供了一个方法 *Math.random()。*这个方法使我们能够返回一个 0 到 1 之间的随机数。当我们使用该方法时，返回值包含 0 但不包含 1(它将返回 1 以内的任何数字)。让我们看一些例子:

```
console.log(Math.random());//Returns ---> 0.26234213885471647console.log(Math.random());//Returns ---> 0.49285095252233835
```

在上面的例子中，我们在控制台日志中调用 Math.random()方法两次。每次我们得到一个不同的随机数返回。

我们可能希望更精确地确定我们想要返回的随机数的范围。例如，如果我们希望返回的随机数在 0 到 10 的范围内，我们可以使用 Math.floor()方法将值向下舍入，然后将 Math.random()的结果乘以 10 并加 1。这方面的一个例子如下所示:

```
console.log(Math.floor(Math.random() * 10) + 1);
//Returns ---> 7console.log(Math.floor(Math.random() * 10) + 1);
//Returns ---> 8
```

如果我们希望返回的随机数在 1 到 100 之间，我们可以遵循类似的过程。

```
console.log(Math.floor(Math.random() * 100) + 1);
//Returns ---> 71console.log(Math.floor(Math.random() * 100) + 1);
//Returns ---> 14
```

我希望您喜欢这篇用 JavaScript 创建随机数的介绍。更多内容请关注我。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*