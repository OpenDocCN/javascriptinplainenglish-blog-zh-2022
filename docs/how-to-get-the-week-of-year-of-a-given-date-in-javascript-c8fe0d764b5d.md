# 获取 JavaScript 中给定日期的一年中的第几周

> 原文：<https://javascript.plainenglish.io/how-to-get-the-week-of-year-of-a-given-date-in-javascript-c8fe0d764b5d?source=collection_archive---------2----------------------->

## 在本文中，我们将看看如何用 JavaScript 获取给定日期的星期。

![](img/db29bf9d425d00bc9b20ef2706baac60.png)

Photo by [Ekaterina Tishkina](https://unsplash.com/@tishkinakaterina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望得到给定日期的一年中的星期。

在本文中，我们将看看如何用 JavaScript 获取给定日期的星期。

# 使用本地 JavaScript 日期方法

获取给定日期的一年中的第几周的一种方法是使用 JavaScript date 方法来计算给定日期的一年中的第几周。

例如，我们可以写:

```
const now = new Date(2021, 3, 1);
const onejan = new Date(now.getFullYear(), 0, 1);
const week = Math.ceil((((now.getTime() - onejan.getTime()) / 86400000) + onejan.getDay() + 1) / 7);
console.log(week)
```

我们有一个`now`日期，我们想从中获得一周中的哪一年。

然后我们创建`onejan`日期，与`now`是同一年的 1 月 1 日。

然后我们通过减去`now`和`onejan`的时间戳来计算一年中的星期。

然后我们用它除以 86400000，得到两个日期之间的天数差。

然后，我们将一周中的某一天加上 1，得到实际的天数差。

然后我们除以 7，得到周数差。

我们用`Math.ceil`将这个数字四舍五入到最接近的整数。

因此，`week`为 14。

# 使用 Moment.js

从给定日期获取一年中的周数的一个更简单的方法是使用 moment.js。

为了使用它，我们写:

```
const now = new Date(2021, 3, 1);
const week = moment(now).format('W')
console.log(week)
```

我们将`now`日期传递给`moment`来创建一个 moment 对象。

然后我们调用带有`'W'`格式化标签的`format`来获取`now`年中的星期。

向下取整，所以`week`是 13。

# 结论

我们可以使用 JavaScript 日期方法或 moment.js 来获取一年中的星期。

*更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，* [***不和***](https://discord.gg/GtDtUAvyhW) *。***