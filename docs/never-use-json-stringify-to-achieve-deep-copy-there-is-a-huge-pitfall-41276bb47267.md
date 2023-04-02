# 千万不要用 JSON.stringify()来实现深度复制。这是一个巨大的陷阱。

> 原文：<https://javascript.plainenglish.io/never-use-json-stringify-to-achieve-deep-copy-there-is-a-huge-pitfall-41276bb47267?source=collection_archive---------7----------------------->

## JSON.stringify()对于深度复制的各种缺陷

![](img/41f1afdca094505fa1aa67ab7db84b2d.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**当对象中有时间类型的元素时——一个*日期*会被转换成*字符串*数据。**

然后你会惊讶的发现 *getTime()* 无法调整， *getYearFull()* 也无法调整。*日期*的所有内置方法都不能调整。但是*字符串*的所有内置方法都可以调用。

**当对象中有*未定义*或*函数*的数据时— — *未定义*和*函数*将直接丢失**

然后你会发现这两种类型的数据都消失了。

**当对象的值为 *NaN* 、 *Infinity* 和 *-Infinity*** 时，对象将变为 *null*

*1.7976931348623157 e+10308*是显示为无穷大的浮点数的最大上线

*-1.7976931348623157 e+10308*是显示为-无穷大的浮点数的最小下线

**当循环对象引用时会报告一个错误**

如果你足够幸运需要复制这样一个对象↓

然后你会发现这些都不起作用。

你还在用 *JSON.stringify()* 实现深度复制吗？

如果是这样，要小心了。作者建议将来使用递归深度复制进行深度复制。

## 摘要

当对象中有一个*日期*时，序列化后会变成一个*字符串*。

如果是对象中的*未定义*和*函数*数据，序列化后会直接丢失。

如果对象中有 *NaN* 、 *Infinity* 、- *Infinity* ，序列化后显示 null。

如果对象被循环引用，它将直接报告一个错误。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**