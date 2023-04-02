# 如何在 JavaScript 中获得两个日期之间的天数

> 原文：<https://javascript.plainenglish.io/how-to-get-the-number-of-days-between-two-dates-in-javascript-373c3343883a?source=collection_archive---------8----------------------->

## 如何用 JavaScript 获得两个日期之间的天数？

![](img/ecf4681ede8a89b385ab1b629b40d1f6.png)

Photo by [Datingjungle](https://unsplash.com/@datingjungle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我们的 JavaScript 应用程序中，我们经常需要得到两个日期之间的天数。

在本文中，我们将看看如何用 JavaScript 获得两个日期之间的天数。

# 使用字符串和日期方法

我们可以通过使用本地字符串和日期方法用 JavaScript 计算两个日期之间的天数。

例如，我们可以写:

```
const parseDate = (str) => {
  const [month, day, year] = str.split('/');
  return new Date(year, month - 1, day);
}const datediff = (first, second) => {
  return Math.round((second - first) / (1000 * 60 * 60 * 24));
}const diff = datediff(parseDate("1/1/2000"), parseDate("1/1/2001"))
console.log(diff)
```

我们有`parseDate`函数，它采用 MM/DD/YYYY 格式的`str`日期字符串。

我们通过用`'/'`作为分隔符分割日期字符串来解析它。

然后通过析构得到`year`、`month`和`day`。

我们将所有这些传递给`Date`构造函数来返回一个日期对象。

我们必须用 1 减去`month`来得到正确的 JavaScript 月份。

然后我们用`dateDiff`方法通过用`first`减去`second`来计算日期差。

当我们减去 2 个日期时，这两个日期都会在相减之前自动转换为时间戳。

所以我们可以直接减去它们。

然后我们用 1 天除以毫秒。

最后，我们用`Math.round`将除法结果四舍五入。

现在我们可以调用我们创建的所有函数来解析并从解析的日期中获取日期差异。

所以我们得到`diff`是 366。

# moment.js

我们可以使用 moment.js 轻松获得两个日期之间的差异。

例如，我们可以写:

```
const start = moment("2000-11-03");
const end = moment("2001-11-04");
const diff = end.diff(start, "days")
console.log(diff)
```

我们只是将日期字符串传递给`moment`函数。

然后我们调用`diff`来获得它被调用的时刻日期和我们传入的时刻日期对象之间的差异。

第二个参数是我们要返回的差值的单位。

所以`diff`也是 366，因为这两个日期相差 366 天。

# 结论

我们可以使用本地 JavaScript 字符串和日期方法来计算两个日期之间的差异。

同样，我们可以使用 moment.js 库来使我们的生活变得更容易。

现在你知道了。感谢您的阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*