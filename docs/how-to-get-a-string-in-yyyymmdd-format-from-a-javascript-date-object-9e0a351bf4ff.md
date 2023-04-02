# 如何从 JavaScript Date 对象中获取 YYYYMMDD 格式的字符串？

> 原文：<https://javascript.plainenglish.io/how-to-get-a-string-in-yyyymmdd-format-from-a-javascript-date-object-9e0a351bf4ff?source=collection_archive---------1----------------------->

## 关于如何将 JavaScript 日期格式化为 YYYYMMDD 格式的字符串的指南。

![](img/9c9cc3d028480907a93e379d4a2343fb.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望将 JavaScript 日期对象转换为 YYYYMMDD 格式的字符串。

在本文中，我们将了解如何将 JavaScript 日期格式化为 YYYYMMDD 格式的字符串。

# 使用本地 JavaScript 日期和字符串方法

将 JavaScript 日期转换成 YYYYMMDD 格式的字符串的一种方法是使用本地 JavaScript 日期和字符串方法。

例如，我们可以写:

```
const date = new Date(2021, 1, 1)
const year = date.getFullYear()
const month = ('0' + (date.getMonth() + 1)).substr(-2)
const day = ('0' + date.getDate()).substr(-2)
const dateStr = [year, month, day].join('')
console.log(dateStr)
```

我们用带有年、月和日的`Date`构造函数创建一个`date`对象。

月份的值从 0 到 11，其中 0 代表一月，1 代表二月，依此类推。

然后我们可以从日期中得到年、月、日。

我们称`getFullYear`为 4 位数年份。

我们调用`getMonth`得到月份，然后加 1 得到人类可读的月份。

然后我们在它前面附加字符串 0，并调用`substr` -2 来获取字符串的最后 2 个字符。

我们调用`getDate`来获取日期，并以与`substr`相同的方式进行格式化。

最后，我们将`year`、`month`和`day`与`join`连接在一起。

所以，`dateStr`就是`'20210201'`。

# 日期.原型. toISOString

我们可以调用`toISOString`从 JavaScript date 对象中获取日期字符串。

然后，我们可以使用字符串方法提取年、月和日期部分，并从该部分中删除破折号。

例如，我们可以写:

```
const date = new Date(2021, 1, 1)
const dateStr = date.toISOString().slice(0, 10).replace(/-/g, "");
console.log(dateStr)
```

我们调用`toISOString`来获取 ISO8601 格式的日期字符串。

然后我们用 0 和 10 调用`slice`提取第一部分，其中有年、月、日。

然后我们调用`replace`用空字符串替换所有破折号来移除它们。

因此，我们对`dateStr`得到相同的结果。

此外，我们可以将`slice`替换为`substring`:

```
const date = new Date(2021, 1, 1)
const dateStr = date.toISOString().substring(0, 10).replace(/-/g, "");
console.log(dateStr)
```

# moment.js

我们还可以使用 moment.js 库轻松设置日期格式。

例如，我们可以写:

```
const date = new Date(2021, 1, 1)
const dateStr = moment(date).format('YYYYMMDD');
console.log(dateStr)
```

我们将`date`传递给`moment`函数，在日期内创建一个 moment 对象。

然后我们用格式字符串调用`format`来格式化该项。

所以我们得到了相同的值`dateStr`。

# 结论

我们可以用原生 JavaScript 日期和字符串方法将原生 JavaScript 日期格式化为字符串。

或者我们可以使用 moment.js 来格式化日期。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*