# 使用 performance.now()测量执行速度

> 原文：<https://javascript.plainenglish.io/use-performance-now-to-measure-execution-speed-150a3a88547d?source=collection_archive---------16----------------------->

## 衡量代码性能的更好方法

![](img/c76d13a14dfec45893b61c93032ed710.png)

Photo by [Abhyuday Majhi](https://unsplash.com/@abhyudaymajhiphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中的`performance.now()`方法可以用来测试代码的性能。这个方法可以用来检查代码的执行时间。

它返回时间的毫秒值(double 类型)。从执行开始的时间由返回值表示。

## performance.now()之前

检查代码性能的古老方法是在代码执行前后使用`Date()`。下面的代码演示了这一点:

```
const start = new Date();for(let i = 0; i < 100000; i++) {
    tasks[i].doSomethingHeavy();
}const end = new Date();const time = start.getTime() - end.getTime();
// use time to measure performance
```

> 此代码仅用于演示目的。当您尝试执行时，它可能不会执行。

所以在这里，我们将执行`for`循环前的时间保存在`start`变量中，并将执行`for`循环后的当前时间记录在`end`变量中。然后我们简单地得到`start`和`end`之间的差值，找出我们的`for`循环执行了多长时间。

## 更好的方法:使用性能。现在

现在，看看下面的代码片段。

```
const start = performance.now();        // UPDATEDfor(let i = 0; i < 100000; i++) {
    tasks[i].doSomethingHeavy();
}const end = performance.now();           // UPDATEDconst time = start - end;                // UPDATED
// use time to measure performance
```

`performance.now()`提供的时间戳不限于一毫秒的分辨率，不像 JavaScript 提供的其他计时数据(例如，`Date.now`)。相反，它们使用具有微秒精度的浮点值来表示时间。

与`Date.now()`相反，`performance.now()`提供的值以稳定的速率增加，与系统时钟无关(可以手动调整或通过 NTP 等软件调整)。否则`performance.timing.navigationStart + performance.now()`之和会接近`Date.now ()`。

**要了解更多关于** `**performance.now()**` **，点击** [**这里**](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now) **。**

这就是这篇文章的内容。我希望你今天学到了一些新东西。您可以在[媒体](https://gouravkajal.medium.com/membership)上[关注我](https://gouravkajal.medium.com/)或者在 [LinkedIn](https://www.linkedin.com/in/gouravkajal/) 上与我联系。想看更多这样的文章，敬请期待！

感谢阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*