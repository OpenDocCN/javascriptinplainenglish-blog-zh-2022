# 如何用 JavaScript 将秒数转换成 hh:mm:ss 格式的时间字符串？

> 原文：<https://javascript.plainenglish.io/how-to-the-number-of-seconds-to-a-time-string-in-the-hh-mm-ss-format-with-javascript-6a758e3a5d99?source=collection_archive---------4----------------------->

![](img/260efb6a041f767f9f953861edee8ee0.png)

Photo by [Sonja Langford](https://unsplash.com/@sonjalangford?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在 JavaScript 应用程序中将经过的秒数转换为 hh:mm:ss 格式的时间字符串。

在本文中，我们将了解如何将秒数转换成 hh:mm:ss 格式的时间字符串。

# 创建我们自己的函数

我们可以创建自己的函数，将经过的秒数转换成 hh:mm:ss 格式的时间字符串。

例如，我们可以写:

```
const toHHMMSS = (numSecs) => {
  let secNum = parseInt(numSecs, 10);
  let hours = Math.floor(secNum / 3600).toString().padStart(2, '0');
  let minutes = Math.floor((secNum - (hours * 3600)) / 60).toString().padStart(2, '0');;
  let seconds = secNum - (hours * 3600) - (minutes * 60).toString().padStart(2, '0');;
  return `${hours}:${minutes}:${seconds}`;
}console.log(toHHMMSS(1234))
```

在`toHHMMSS`函数中，我们将`numSecs`参数解析成一个数字。

然后我们通过将`secNum`除以 3600 来计算时间。

然后我们用`Math.floor`将其向下舍入到最接近的整数。

然后我们在它上面调用`toString`，把它转换成一个字符串。

然后我们调用`padStart`将数字串填充为两位数，如果需要的话，在前面加一个零。

为了计算`minutes`，我们用`hours`乘以 3600 减去`secNum`，然后除以 60。

减去小时后我们得到分钟数。

我们用`Math.floor`将数字向下舍入到最接近的整数。

然后我们也用`padStart`把它填充到一个 2 位数的字符串中。

接下来，我们通过从`secNum`中减去转换成秒的`hours`和`minutes`来计算`seconds`。

然后我们将它转换成一个字符串，并在其上调用`padStart`来填充字符串到 2 位数，如果需要的话，在前面加一个零。

最后，我们返回字符串中的`hours`、`minutes`和`seconds`。

因此，控制台日志应该记录:

```
'00:20:34'
```

# 日期.原型. toISOString

我们可以调用 JavaScript date 对象上的`toISOString`来获得一个包含小时、分钟和秒的日期字符串。

要获得经过的时间，我们只需创建一个时间戳为 0 的日期，然后调用`setSeconds`将时间戳设置为经过的秒数。

然后我们都可以`toISOString`获取日期字符串，并提取返回的日期字符串的小时、分钟和秒部分。

例如，我们可以写:

```
const date = new Date(0);
date.setSeconds(1234);
const timeString = date.toISOString().substr(11, 8);
console.log(timeString)
```

我们创建一个时间戳为 0 的`Date`实例。

然后我们调用`setSeconds`来设置时间的秒。

然后我们调用`toISOString`来获得一个日期字符串。

然后我们调用`substr`来提取小时、分钟和秒的子串。

因此，`timeString`是:

```
'00:20:34'
```

# 结论

我们可以使用数学、日期和字符串方法，通过 JavaScript 轻松地将经过的秒数转换成 hh:mm:ss 格式。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***