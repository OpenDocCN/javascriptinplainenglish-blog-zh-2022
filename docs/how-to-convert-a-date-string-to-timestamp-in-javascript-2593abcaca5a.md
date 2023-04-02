# 如何在 JavaScript 中将日期字符串转换成时间戳？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-date-string-to-timestamp-in-javascript-2593abcaca5a?source=collection_archive---------1----------------------->

## JavaScript 中将日期字符串转换为时间戳的不同方法。

![](img/90ff34074edcde0cb8d30193d7a0df17.png)

Photo by [Aron Visuals](https://unsplash.com/@aronvisuals?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望用 JavaScript 将日期转换成 UNIX 时间戳。

在本文中，我们将研究用 JavaScript 将日期转换成时间戳的方法。

# 使用 Date.parse()方法

我们可以使用`Date.parse()`方法将日期字符串转换成时间戳。

例如，我们可以写:

```
const toTimestamp = (strDate) => {
  const dt = Date.parse(strDate);
  return dt / 1000;
}
console.log(toTimestamp('02/13/2020 23:31:30'));
```

我们创建了`toTimestamp()`方法，该方法调用带有日期字符串的`Date.parse()`方法，将其解析成时间戳。

单位是毫秒，所以我们必须用它除以 1000 来转换成秒。

# 使用 getTime()方法

我们可以使用`Date`实例的`getTime()`方法将日期字符串转换成时间戳。

为了使用它，我们写:

```
const toTimestamp = (strDate) => {
  const dt = new Date(strDate).getTime();
  return dt / 1000;
}
console.log(toTimestamp('02/13/2020 23:31:30'));
```

我们用`Date`构造函数创建了`Date`实例。

然后我们调用`getTime()`以毫秒为单位返回时间戳。

所以我们必须把它除以 1000，得到秒数。

# Moment.js 的 unix()方法

我们可以使用 Moment.js 的`unix()`方法返回一个时间戳。

例如，我们可以写:

```
const toTimestamp = (strDate) => {
  const dt = moment(strDate).unix();
  return dt;
}
console.log(toTimestamp('02/13/2020 23:31:30'));
```

我们将`strDate`传递给`moment()`函数，返回一个带有时间的力矩对象。

然后我们可以在上面调用`unix()`方法来返回时间戳。

`unix()`方法返回以秒为单位的时间戳，因此我们不必将返回的结果除以 1000。

# 结论

我们可以使用普通 JavaScript 或 Moment.js 将日期字符串转换成 UNIX 时间戳。

*更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***