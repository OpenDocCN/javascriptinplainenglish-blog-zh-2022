# JavaScript 中的日期方法是什么

> 原文：<https://javascript.plainenglish.io/what-are-the-dates-methods-in-javascript-b69245f4c8ae?source=collection_archive---------7----------------------->

## Java Script 语言

## 如何使用 JavaScript 日期

![](img/4fe645dcdae0ecac2e8c58e9e361d76f.png)

Photo by [Towfiqu barbhuiya](https://unsplash.com/@towfiqu999999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 日期可能很难处理，因为它们很复杂。这看起来并不困难，但是记住它们是关键。与 Node.js 框架不同，普通的 JavaScript 日期没有像`.add()`或`.subtract()`这样的方法，任何数字都是天数或年数。

## 初始化日期

创建/初始化新日期有 4 种具体方法。

`new **Date**()` —通过这种方式，您可以在脚本文件中调用该方法时创建新的日期。`new Date()`收益的一个例子—

`Mon Jun 13 2022 16:59:37 GMT+0200 (CEST)`。

`new **Date**(millisecond)` —这样，您可以从日期`January 1, 1970`开始添加以毫秒为单位的新日期。`new **Date**(1000)`收益的一个例子—

`Thu Jan 01 1970 01:00:01 GMT+0100 (CEST)`。

`new **Date**(date_string)` —这样，您可以通过向其传递一个日期字符串来创建一个新日期，该字符串将被解析。一个日期字符串的例子—

`"January 8, 2020 15:00:00"`。

`new **Date**(year, month, day, hour, minute, second)` —这样，您可以基于传递给它的几个属性创建一个新日期。如果您不想要当前时间，这是创建日期的最佳方式。

参数的数量可以是 2-6，从左侧传递。月份的指数为 0，因此月份可以是 0-11。

`new **Date**(2020, 0, 8, 15, 0, 0)`返回的一个例子— `Wed Jan 08 2020 15:00:00 GMT+0100 (CEST)`。

# 日期方法

这里列出了您可以在项目中使用的与 JavaScript 中的日期结构相关的最重要和最有用的方法。

## 与日期相关的

![](img/3f7c9297b9b6fe9e660701f0abecd633.png)

Photo by [Debby Hudson](https://unsplash.com/@hudsoncrafted?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`.getFullYear()` —返回整年，例如:`2020`

`.getMonth()` —返回一年中的月份索引(0–11)，例如:`0`

`.getDate()` —返回一个月中的某一天，例如:`31`

`.getDay()` —返回一周中的日索引(0–6)，例如:`6`

## 与时间相关的

![](img/17a490c3d6940274c4b44a8d17f87c25.png)

Photo by [Lukas Blazek](https://unsplash.com/@goumbik?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`.getHours()` —返回小时数，例如:`15`

`.getMinutes()` —返回分钟数，例如:`20`

`.getSeconds()` —返回秒，例如:`35`

`.getTime()` —返回自`January 1, 1970`以来以毫秒为单位的日期，例如:`1636725600000`

## 与地区相关的

![](img/1a5c05add96c82b794a527f9d1c9a056.png)

Photo by [delfi de la Rua](https://unsplash.com/@delfidelarua7?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`.toLocaleString()` —返回日期和时间的复合字符串，例如:`11/12/2021, 3:00:00 PM`

`.toLocaleDateString()` —返回简单的日期格式，例如:`11/12/2021`

`.toLocaleTimeString()` —返回简单的时间格式，例如:`3:00:00 PM`

## 集合相关的

您可以按照与获取参数类似的方式设置日期的各个参数，只需将方法`get` → `set`中的关键字替换为相应的参数。比如`.getHours()` → `.setHours(hours)`。

## UTC 相关

如果您想要获取/设置日期的某个部分，我们可以用与获取和设置它们类似的方式来完成，只需在`get` / `set`之后添加一个`UTC`关键字。比如`.getFullYear()` → `.getUTCFullYear()`。

# 结论

日期对于运行日期和时间相关的例程非常重要。如果你正在使用 Node.js，最好安装一个 NPM 库来处理你的日期，比如`Moment.js`。如果您使用普通的 JavaScript，我希望这篇文章能帮助您理清思路。你可以随时回到这里，把它作为你的小抄。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*