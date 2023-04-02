# 如何将 JavaScript 日期初始化为特定的时区？

> 原文：<https://javascript.plainenglish.io/how-to-initialize-a-javascript-date-to-a-particular-time-zone-a03969601c58?source=collection_archive---------2----------------------->

![](img/6f80996fe80a7630310ee62d0a5ba4e9.png)

Photo by [Lukas Blazek](https://unsplash.com/@goumbik?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望将 JavaScript 日期初始化为特定的时区。

默认时区是 UTC。

在本文中，我们将研究将 JavaScript 日期初始化为特定时区的方法。

# 将时区添加到日期字符串的末尾

我们可以将时区信息添加到用于创建`Date`对象的日期字符串的末尾。

例如，我们可以写:

```
const d = new Date("2020-04-13T00:00:00.000+08:00");
console.log(d)
```

`+08:00`部分意味着我们拥有的日期字符串比 UTC 早 8 小时。

所以`d`是:

```
Sun Apr 12 2020 09:00:00 GMT-0700 (Pacific Daylight Time)
```

当我们使用设置为太平洋时区的设备时。

# Date.prototype.toLocaleString

JavaScrip date 对象具有`toLocaleString`方法，用于将日期转换为给定时区的日期字符串。

例如，我们可以写:

```
const d = new Date("2020-04-13T00:00:00.000+08:00");
const dateStr = d.toLocaleString('en-US', {
  timeZone: 'America/New_York'
})
console.log(dateStr)
```

来做这个。

我们在`d`上调用`toLocaleString`，第一个参数是地区。

第二个参数是一个属性设置为`'America/New_York'`的对象，这样我们可以返回纽约时区的日期字符串。

因此，`dateStr`是:

```
4/12/2020, 12:00:00 PM
```

这相当于我们传递给纽约时区的`Date`构造函数的日期和时间。

# 获取小时数

如果我们用`getHours`得到小时，那么返回的小时将与设备的时区相同。

例如，如果我们有:

```
const d = new Date("2020-04-13T00:00:00.000+08:00");
console.log(d.getHours())
```

字符串中的时间是午夜。

时区是 UTC +8。

因此，如果我们在太平洋时区，我们得到 9，因为它是夏令时，所以它比 UTC 晚 7 个小时，比 UTC +8 晚 15 个小时。

# 结论

我们可以通过将时区信息添加到用于在 JavaScript 中创建`Date`实例的日期字符串中来初始化具有给定时区的日期。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*