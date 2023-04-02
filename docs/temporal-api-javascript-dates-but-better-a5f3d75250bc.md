# 时态 API: JavaScript 日期，但更好

> 原文：<https://javascript.plainenglish.io/temporal-api-javascript-dates-but-better-a5f3d75250bc?source=collection_archive---------2----------------------->

![](img/14a174b7d5a733433abe90695c8a2f17.png)

Photo by [Aron Visuals](https://unsplash.com/@aronvisuals?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/time?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

如果你曾经在 JavaScript 中处理过日期，你肯定知道处理它们有多麻烦和困难；这就是为什么，最近，有一个全新的工作方式的建议，你已经猜到了——时态 API。

现在，这是什么？

如果我们利用他们提供的介绍性信息，

> `Date`一直是 ECMAScript 长期以来的痛点。这是对`Temporal`的提议，它是一个充当顶级名称空间的全局`Object`(就像`Math`)，为 ECMAScript 语言带来了一个现代的日期/时间 API。要详细了解`Date`的一些问题，以及时态的动机，请参见:[修复 JavaScript 日期](https://maggiepint.com/2017/04/09/fixing-javascript-date-getting-started/)。

## 你为什么想用它？

嗯，有几个原因，比如:

*   一个更容易使用的 API，包括时间和日期
*   直观的命名约定(`Plain` / `Zoned`，取决于您是否需要时区不可知论)
*   提取时间/日期差异的简易性
*   字符串和对象格式之间的互操作性
*   只需要处理代表时间或日期的对象

我相信新的时态 API 为我们提供了很多以前 JS Dates 所缺乏的实用程序(必须通过库来弥补，如[***moment . JS***](https://momentjs.com)或[***date-fns***](https://date-fns.org))，以及一种更好的处理单个全局日期对象(`Temporal`)的方式。

## 时态 API 数据类型

使用时态 API 时要考虑的一个重要因素是，它提供的数据类型被分成`Plain` & `Zoned`:

*   `**Plain**`，不提供时区信息
*   `**Zoned**`，表示日期/时间，信息绑定到特定时区；它最适合于需要处理特定时区内的特定时间的场景，或者需要进行格式化，或者执行考虑时区特定信息的时间/日期差异/加法运算的场景

您最有可能使用的一些关键数据类型:

## **1。普通日期时间**

这是最容易理解的方法之一，因为它表示一个没有附加时区信息的日期和时间对象。您可以通过使用`Temporal.Now.plainDateTimeISO`方法简单地创建一个实例。

这个方法创建一个新的使用本地时区日期&时间的`PlainDateTime`对象，除非没有其他时区参数传递给这个方法。

## 2.普通约会

该对象包含没有附加时区数据的日期信息。它最适合不需要任何时间信息的情况。

## 3.哀怨

一个`PlainTime`对象表示一个没有日期或时区信息的时间。关于这种数据类型，需要注意的是没有关联的`Temporal.Now.plainTime`方法，因为对于`PlainTime`对象来说，没有特定的日历上下文。

## 4.ZonedDateTime

`ZonedDateTime`对象是一个 datetime 对象，它打包了所有与时区相关的信息，这使得它非常适合需要夏令时的情况。

## 5.瞬间

在表示特定时间点方面，`Instant`对象类似于`ZonedDateTime`对象，但是不同之处在于它总是包含 UTC 时间，并且不引用特定的日历。

您也不能将一个对象传递给`Instant`的`from`方法(我将在一秒钟内解决这个问题),当您将一个字符串传递给`from`方法时，它必须包含时区信息。

## 6.`PlainMonthDay`

一个`PlainMonthDay`就像一个`PlainDate`，唯一的区别是它不包括任何年份信息。这在处理节假日(12 月 25 日)等总是在同一天的事情时尤其有用。

因为这是一种不太常见的数据类型，所以创建它的唯一方法是使用`from`方法和构造函数。

## 7.平年月份

与`PlainMonthDay`类似，`PlainYearMonth`对象具有完全相同的效用，除了这次您处理的是月份&年份。

## 时态 API 提供的实用方法

如果我们只有这些数据类型而没有其他，那有什么好处呢？这就是为什么 Temporal API 附带了各种非常有用的实用方法来弥补 JavaScript Dates 目前所缺乏的功能。

## 1.加/减

在 JavaScript 中添加或减去日期的一部分确实很烦人，但是使用时态 API，我们到目前为止讨论的所有数据类型都内置了`add`和`subtract`方法，这让事情变得非常简单。

这两个函数有完全相同的参数，唯一的区别是一个是加法，而另一个是减法。

使用这些方法最简单的方法是通过向`add` / `subtract`方法传递一个对象，该对象带有您想要进行的更改的属性。

这些函数的另一个好处是它们会自动处理溢出。

例如，如果您尝试在 1 月 31 日的日期上加 1 个月，结果会是不存在的 2 月 31 日。默认情况下，这些结果将被固定到最近的有效日期，因此它将返回 2 月 28 日。

您也可以禁用这种行为，不过要使用第二个选项参数。

## 2.自/直到

`since`和`until`方法将确定当前时态日期对象和另一个时态日期对象之间的时间距离。

类似于`add`和`subtract`,`since`和`until`方法彼此相反，并采用完全相同的参数。

这些方法返回的值是一个`Temporal.Duration`对象。此外，您可以向这些方法传递一个选项参数，以真正微调您希望如何计算持续时间。

如果您指定了`largestUnit`，那么将使用该单位作为最大值而不是默认值来指定持续时间。

如果您指定了`smallestUnit`，那么将使用该单位作为最小值而不是默认值来指定持续时间。这可能导致舍入，可通过`roundingIncrement`和`roundingMode`选项进一步定制。

## 3.等于

最后的方法有点复杂，所以让我们看看一个非常简单的方法。

如果两个时态日期对象具有完全相同的字段，则`equals`方法将返回 true。这是必要的，因为从技术上讲，用`==`或`===`进行的任何比较都是假的，除非这两个对象是同一个实例。

## 4.随着

这是我最喜欢的助手方法之一，因为它覆盖了 JavaScript 日期中的一个巨大弱点。`with`方法接受一个字段对象来覆盖当前日期对象。

此外，关于这个方法需要知道的重要的一点是，它实际上并不改变它所调用的时态日期对象。相反，它返回一个新的时态日期对象，并对其应用更改。

## 5.轮次

`Round`是一个方法，当在一个类似于`Temporal`的对象上调用时，它返回一个新的日期/时间对象，该对象由参数指定的特定单位舍入。

如果您想修改舍入的执行方式，您可以传递一个带有`smallestUnit`、`roundingIncrement`和`roundingMode`参数的对象。

## 6.比较

我想谈的最后一个方法是`compare`方法，它适用于实际的数据类型，而不是对象实例。这种方法非常常用于简化日期排序。

## 其他数据类型

到目前为止，我们已经查看了该节目的明星，但还有一些数据类型，虽然您可能不会经常使用，但了解这些数据类型是很有用的。

## 1.持续时间

我们在本文中提到过几次的`Duration`数据类型。这种数据类型只是表示一段时间，通常不是您自己构建的，而是在比较日期时需要处理的。但是，如果您愿意，可以用构造函数或`from`方法创建一个新的持续时间。

与前面提到的其他数据类型类似，您也可以对持续时间使用`add`、`subtract`、`with`和`round`方法。还有一些您想知道的额外的帮助器方法:

## 2.时区

`TimeZone`数据类型用于表示特定的时区。您最可能使用它的场景是使用`from`方法或`Temporal.Now.timeZone`方法，但是您也可以使用构造函数。

该数据类型最重要的助手函数是`getNextTransition`和`getPreviousTransition`，它们将返回下一次/上一次夏令时转换的日期/时间。

## 3.日历

`Calendar`数据类型是您需要知道的最后一种数据类型，可能也是最没用的。您可以使用`from`方法创建一个日历，或者如果您愿意，也可以使用构造函数。

对于这种数据类型，您真的不需要知道什么重要的函数，因为您真的不太可能经常使用它。

## 浏览器支持

希望在阅读完所有这些之后，您会兴奋地开始尝试时态 API。我得到的唯一坏消息是这个 API 还不可用，因为它还在提议阶段 3。目前还没有浏览器支持这个 API，但是如果你想现在就开始使用这个 API，你可以使用一个 polyfill。

这个 API 有多个 polyfill，但是我发现 [@js-temporal/polyfill](https://www.npmjs.com/package/@js-temporal/polyfill) 是一个很好的选择。一旦你安装了这个库，你就可以立即开始使用时态 API。

## 最后一句话

我们都知道 JavaScript Dates 可以好得多，我真的相信时态 API 是一个巨大的进步，也是一条路要走。我很高兴我们可以选择试用 Stage 3 时态 API 版本，因为它提供了一些关于一个非常有前途的、可能包含在 JavaScript 未来版本中的项目的见解。

我希望这篇文章对您有用，并且激发了您对用 JavaScript 处理日期的新方法的兴趣。

如果你愿意支持我当作家，可以考虑报名成为 [***中等会员***](https://vlad-mihet.medium.com/membership) 。每月只需 5 美元，你就可以无限制地阅读我和其他作家在 Medium 上的所有文章。

如果你喜欢看这篇文章，你也可以在这里给我买杯咖啡来支持我。

***你可能会感兴趣的我的其他一些故事:***

[*你可以学到的 3 件最重要的事情*](https://vlad-mihet.medium.com/the-3-most-important-things-that-you-can-learn-51825ccb8dde)

[*软件开发什么时候需要创造力？*](https://vlad-mihet.medium.com/when-is-creativity-needed-in-software-development-b97ed53311a5)

[](https://vlad-mihet.medium.com/6-months-as-a-software-engineer-coming-from-freelancing-d4f6626b01ab)*自由职业 6 个月软件工程师*

*[*为什么我觉得所有的开发者都应该有自由职业的味道？*](https://vlad-mihet.medium.com/web-dev-freelancing/why-do-i-think-all-developers-should-have-a-taste-of-freelancing-465a58d8d2ce)*

*[*每当我在职业生涯中失去提升的动力时，我会怎么做？*](https://vlad-mihet.medium.com/what-do-i-do-whenever-i-lose-motivation-for-improvement-in-my-career-a4c076ae3413)*

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。******