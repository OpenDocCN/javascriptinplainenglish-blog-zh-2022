# Moment.js 中 7 个有用的方法

> 原文：<https://javascript.plainenglish.io/7-useful-methods-in-moment-js-5917592bb6c6?source=collection_archive---------15----------------------->

## 如何正确使用 Node.js 库 Moment.js

![](img/a8a29044d6b43c868574065fbd2f2d5c.png)

Photo by [Agê Barros](https://unsplash.com/@agebarros?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Moment.js 是一个 Node.js 框架，能够解析和操作日期及其时间。它是处理日期时最常用的框架之一，今天我们将看看这个框架能提供的最有用的方法。

# 安装软件包

我们可以通过在项目的目录控制台中键入这个命令来安装这个包。然后，我们可以通过键入以下命令在 JavaScript 文件中要求该模块:

`const **moment** = **require**('moment');`

# 从语法上分析

瞬间。JS 使用解析将任何可能的值从字符串、日期、UTC 或其他格式转换成一个时刻日期值。

## 现在

要获得当前的日期和时间值，我们可以简单地从包中调用导入的变量— `**moment**()`。

## 字符串值

我们可以从传递给它的字符串值中创建一个时刻日期。支持的字符串有`ISO 8601`、`RFC 2822`以及更多组合。比如`**moment**('2013-02-08')`。

但是如果我们想给日期加上一个时间，我们可以用一个`space character`或`T`来分隔，例如`**moment**('2013-02-08 09:30')`。

你可以在这里找到更多关于字符串值[类型的信息。](https://momentjs.com/docs/#/parsing/string/)

## 字符串值和格式

我们可以用一组预定义的字符直接格式化日期字符串值来修改输出。传递字符串值后，可以将格式设置为第二个参数。

比如`**moment**('12-25-1995', 'MM/DD/YYYY')`会返回`12/25/1995`。

你可以在这里找到更多关于字符集[的信息。](https://momentjs.com/docs/#/parsing/string-format/)

# 操纵

您可以通过加减任意数量的分钟、天数、月数和/或年数来操作日期的输出。

## 加

我们可以将任意数量的日期值添加到某个时刻的日期中，并获得相加后的输出。方法`add()`是一个带有两个参数的连接方法— `**add**(amount, date-type)`。

参数`amount`是我们想要添加多少个日期类型，参数`date-type`是我们想要添加什么日期类型。

比如`**moment**('12-25-1995').**add**(7, 'days')`。

## 减法

我们可以减去某个时刻日期的任意数量的日期值，并通过相减得到输出。方法`subtract()`是一个带有两个参数的连接方法——`**subtract**(amount, date-type)`。

参数`amount`是我们想要添加多少个日期类型，参数`date-type`是我们想要添加什么日期类型。

比如`**moment**('12-25-1995').**subtract**(5, 'months')`。

## 时间开始

我们可以找出另一种日期类型将出现的日期/例如，另一个月或年将开始的日期。方法`startOf()`有 1 个参数，那就是日期类型。

比如`**moment**().**startOf**('month')`。

## 时间的终结

和时间的开始一样，时间的结束会告诉你另一个日期类型什么时候结束。方法`endOf()`有 1 个参数，那就是日期类型。

比如`**moment**().**endOf**('year')`。

# **结论**

这个框架有更多本文中没有提到的实用程序，你可以在官方文档[这里](https://momentjs.com/docs/#/parsing/)读到它们。这些是我认为最有用的，我希望你喜欢这篇文章，并在你的下一个项目中使用它们。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*