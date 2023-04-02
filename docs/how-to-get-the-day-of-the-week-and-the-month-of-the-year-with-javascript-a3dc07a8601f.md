# 如何用 JavaScript 获取一年中的星期几和月份？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-day-of-the-week-and-the-month-of-the-year-with-javascript-a3dc07a8601f?source=collection_archive---------4----------------------->

![](img/a83510f7fdccf4a80ba8ddd742048e8b.png)

Photo by [Arindam Saha](https://unsplash.com/@flux_culture?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 得到一周中的某一天和一年中的某一月。

在本文中，我们将看看如何用 JavaScript 获得一周中的某一天和一年中的某一月。

# 获取星期几

为了获得星期几，我们可以使用带有日期字符串数组的`getDay`方法来获得星期几。

例如，我们可以写:

```
const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];const dt = new Date(2021, 1, 1)
const day = days[dt.getDay()];
console.log(day)
```

我们有一个包含日期名称的`days`数组。

然后用`Date`构造函数创建`dt`日期对象。

接下来，我们在`dt`调用`getDay`来获取日索引，从 0 开始表示周日，到 6 表示周六。

我们将它传递给`days`来获得日期的名称。

因此`day`就是`'Monday'`。

# 获取一年中的月份

为了获得星期几，我们可以使用带有日期字符串数组的`getMonth`方法来获得一年中的月份。

例如，我们可以写:

```
const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
const dt = new Date(2021, 1, 1)
const month = months[dt.getMonth()];
console.log(month)
```

我们有包含月份名称的`months`数组。

我们有一个包含日期名称的`days`数组。

然后用`Date`构造函数创建`dt`日期对象。

接下来，我们调用`dt`上的`getMonth`来获取月份索引，从 1 月的 0 到 12 月的 11。

我们将它传递给`months`以获得日期的名称。

因此`month`就是`'February'`。

# 结论

为了获得星期几，我们可以使用带有日期字符串数组的`getDay`方法来获得星期几。

为了获得星期几，我们可以使用带有日期字符串数组的`getMonth`方法来获得一年中的月份。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*