# 如何在 JavaScript 中实现 sleep()函数？

> 原文：<https://javascript.plainenglish.io/how-can-you-implement-the-sleep-function-in-javascript-db5d4d89b13b?source=collection_archive---------3----------------------->

## 如何在 JavaScript 中实现 sleep()函数的指南。

![](img/9b988bb462e4b79e68bcddbf989b8ca0.png)

# 大家好👋

朋友们好，我是**雪球**。我是一个年轻的热情和自学前端网站开发人员，并打算成为一名成功的开发人员。

今天，我再次在这里提出一个惊人的话题，你会喜欢阅读。所以让我们开始吧！🚀

# 🌟介绍

默认情况下，Javascript 不附带`sleep()`函数。为了实现睡眠定时器，`setTimeout()`函数最接近于`sleep()`函数。还有其他一些不太常见的方法来实现睡眠功能，以在某个特定的持续时间后创建暂停。

# 设置超时

`setTimeout()`为超时后执行一次代码的功能设置定时器。唯一在`setTimeout()`函数中的代码将在给定的时间后执行。持续时间总是以**毫秒(ms)** 为单位。下面是如何编写`setTimeout()`函数的方法。

```
const printHelloWorld = () => {
  console.log("Hello");
  setTimeout(() => console.log("World"), 500);
};printHelloWorld(); // "Hello", "World" ("World" logs after 500ms)
```

# 同步方法

这里，我们可以使用一个循环来停止函数的执行

```
const sleep = (ms) => {
  const stop = new Date().getTime() + ms;
  while (new Date().getTime() < stop) {}
}const printHelloWorld = () => {
  console.log("Hello");
    sleep(500)
  console.log("World")
};printHelloWorld(); // "Hello", "World" ("World" logs after 500ms)
```

# 异步方法

使用`async`和`await`以及`setTimeout()`和`Promise`实现`sleep()`功能的干扰较少的方法。因为我们处理的是`Promise`，所以执行函数必须是`async`。

```
const sleep = (ms) =>
  new Promise(resolve => setTimeout(resolve, ms));const printHelloWorld = () => {
  console.log("Hello");
    sleep(500)
  console.log("World")
};printHelloWorld(); // "Hello", "World" ("World" logs after 500ms)
```

所以，这就是这篇文章。我希望你学到了新的东西，并喜欢阅读。敬请关注下一篇文章。

我们在推特上连线— [@codewithsnowbit](https://twitter.com/codewithsnowbit)

# 🌏让我们连接

*   [GitHub](https://github.com/codewithsnowbit)
*   [推特](https://twitter.com/codewithsnowbit)
*   [YouTube](https://www.youtube.com/channel/UCNTKqF1vhFYX_v0ERnUa1RQ?view_as=subscriber)
*   给我买杯咖啡

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*