# 在 JavaScript 中使用日期和时间

> 原文：<https://javascript.plainenglish.io/using-date-and-time-in-javascript-5383a3670303?source=collection_archive---------7----------------------->

## JavaScript 中使用日期和时间的介绍

![](img/d99d9e7e9816fa8c618b59a243c46bdb.png)

## **简介**

在 JavaScript 中，当我们想要处理日期和时间时，可以使用 Date 对象。为了使用日期对象，我们使用日期对象构造函数，如下例所示。默认情况下，这将返回当前日期和时间。

```
new Date()
Sun Sep 11 2022 14:44:19 GMT+0100 (British Summer Time)
```

上面的例子可以存储在一个变量中，但是它总是存储变量创建的日期和时间。

```
let currentDate = new Date();
console.log(currentDate);//Returns ---> Sun Sep 11 2022 14:45:28 GMT+0100 (British Summer Time)
```

## 警告

在 JavaScript 中处理日期时，需要考虑一些注意事项。日期和时间是根据计算机的时钟计算的。这意味着如果另一个用户在不同的国家和时区，那么这可能会导致一天开始的时间发生冲突。

## 方法

使用 Date 对象时，可以设置日期或时间的格式。我们现在来看一些例子。我们将首先创建一个名为 current date 的变量，并为其分配 date 对象。

```
let currentDate = new Date();
//Returns --> Sun Sep 11 2022 14:49:46 GMT+0100 (British Summer Time)
```

现在，如果我们只想从返回值中访问日期，我们可以使用另一个名为 getDate()的方法。

```
currentDate.getDate();
//Returns 11
```

我们还可以通过使用 getTime()方法来访问时间。

```
currentDate.getTime();
//Returns ---> 1662904186833
```

还可以通过使用返回人类可读的时间字符串的方法来进一步格式化时间。这个方法是 toTimeString()。

```
currentDate.toTimeString();
//Returns ---> '14:49:46 GMT+0100 (British Summer Time)'
```

还有一个方法将返回人类可读的日期字符串。这个方法称为 toDateString()。

```
currentDate.toDateString();
//Returns ---> 'Sun Sep 11 2022'
```

我之前提到过使用 Date 对象时的时区警告。getTimezoneOffset()是一个根据地区(语言)返回分钟偏移量的有用方法。

```
currentDate.getTimezoneOffset();
//Returns ---> -60
```

## 创建自定义时间

当您处理日期和时间时，您可能会希望创建自己的日期和时间。您可以通过在创建 Date 对象时向其传递值来实现这一点。如果我们有一个出生于 2001 年 9 月 8 日的用户，我们可以这样做，如下所示。

```
const bobby = new Date(2001, 8, 9);
console.log(bobby);//Returns ---> Sun Sep 09 2001 00:00:00 GMT+0100 (British Summer Time)
```

创建自定义日期时，传递给 Date 对象的值的顺序如下。顺便说一下，这个月从零开始计数。所以，一月是 0，二月是 1，以此类推。

*YYYY，MM，DD，HH，MM，SS*

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更内容于* [***普通英语***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*以及*[**T42 不和**](https://discord.gg/GtDtUAvyhW) *上跟随我们。对增长黑客感兴趣？查看* [***电路***](https://circuit.ooo/) *。**