# 用 Moment.js 把 UNIX 时间戳转换成日历日期？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-unix-timestamp-to-a-calendar-date-with-moment-js-e27100819553?source=collection_archive---------4----------------------->

## 关于如何使用 Moment.js 将 UNIX 时间戳转换为日历日期的教程

![](img/1a36765e6b9126b8f68113b92a7d86cc.png)

Photo by [Max Rosero](https://unsplash.com/@mrosero?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 Moment.js 将 UNIX 时间戳转换成日历日期。

在本文中，我们将研究如何使用 Moment.js 将 UNIX 时间戳转换为日历。

# 使用 unix()和 format()方法

我们可以使用`unix()`方法从时间戳创建一个 moment 对象。

然后我们可以使用`format()`方法将日期格式化为日历日期。

例如，我们可以写:

```
import moment from 'moment'
const dt = +new Date(2021,1,1)
const dateString = moment.unix(dt / 1000).format("MM/DD/YYYY");
console.log(dateString)
```

我们用`Date`构造函数创建了`dt`日期对象。

然后我们用一元的`+`操作符将它转换成以毫秒为单位的时间戳。

接下来，我们调用带有以秒为单位的时间戳的`moment.unix()`。

然后我们调用`format()`将日期格式化为 MM/DD/YYYY 格式。

所以`dateString`就是`‘02/01/2021’`。

# 使用 moment()函数和 format()方法

我们可以只使用`moment()`函数而不使用`unix()`方法来从时间戳创建一个 moment 对象。

例如，我们可以写:

```
import moment from 'moment'
const dt = +new Date(2021,1,1)
const dateString = moment(dt).format("MM/DD/YYYY");
console.log(dateString)
```

`moment()`函数采用以毫秒为单位的时间戳。

所以我们传入的时候不用把`dt`除以 1000。

代码的其余部分是相同的，我们得到的结果和以前一样。

# 结论

我们可以用`format()`的`moment()`函数或者`unix()`的`format()`方法将时间戳转换成日历日期。

这就是了。感谢您的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***