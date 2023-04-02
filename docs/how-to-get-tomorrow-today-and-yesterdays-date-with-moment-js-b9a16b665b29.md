# 如何用 Moment.js 获取明天，今天，昨天的日期

> 原文：<https://javascript.plainenglish.io/how-to-get-tomorrow-today-and-yesterdays-date-with-moment-js-b9a16b665b29?source=collection_archive---------3----------------------->

![](img/e21323c58bb8d47f9351e0df04699f79.png)

Photo by [Christian Englmeier](https://unsplash.com/@christianem?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 moment.js 获取明天、今天或昨天的日期。

在本文中，我们将了解如何使用 moment.js 获取明天、今天或昨天的日期。

# 获取今天的日期

我们可以用`moment`函数得到今天的日期。

然后我们可以用`format`方法将其格式化为人类可读的日期字符串。

例如，我们可以写:

```
const today = moment();
console.log(today.format('YYYY-MM-DD'))
```

创建`today`变量，该变量被设置为带有今天日期的 moment 对象。

然后我们用`'YYYY-MM-DD'`调用`format`将日期格式化为 YYYY-MM-DD 格式。

# 获取明天的日期

我们可以用`moment`函数和`add`方法得到明天的日期。

然后我们可以用`format`方法将其格式化为人类可读的日期字符串。

例如，我们可以写:

```
const tomorrow = moment().add(1, 'days');
console.log(tomorrow.format('YYYY-MM-DD'))
```

创建`tomorrow` 变量，该变量被设置为带有今天日期的 moment 对象。

然后我们用 1 调用`add`，用`'days'`给今天加一天。

然后我们用`'YYYY-MM-DD'`调用`format`将日期格式化为 YYYY-MM-DD 格式。

# 获取昨天的日期

我们可以用`moment`函数和`add`方法得到明天的日期。

然后我们可以用`format`方法将其格式化为人类可读的日期字符串。

例如，我们可以写:

```
const yesterday = moment().add(-1, 'days');
console.log(yesterday.format('YYYY-MM-DD'))
```

创建设置为带有今天日期的 moment 对象的`tomorrow` 变量。

然后我们用-1 调用`add`，用`'days'`减去一天到今天。

然后我们用`'YYYY-MM-DD'`调用`format`将日期格式化为 YYYY-MM-DD 格式。

# 结论

我们可以用 moment.js 轻松计算明天、今天或昨天。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***