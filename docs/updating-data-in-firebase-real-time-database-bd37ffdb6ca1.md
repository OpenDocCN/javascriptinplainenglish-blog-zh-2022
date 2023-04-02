# 如何更新 Firebase 实时数据库中的数据

> 原文：<https://javascript.plainenglish.io/updating-data-in-firebase-real-time-database-bd37ffdb6ca1?source=collection_archive---------24----------------------->

因为我们犯了一个错误，希望你不会。

![](img/9b32f56e3a732c6e5c41f9a8eaae65d0.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在后台

这个故事的议程很简单——我们面对一个问题，并找到了解决方案，所以我们想分享它。我们最近在我们的网站上发布了日志部分，为用户提供了一个只阅读我们在网站上写的每一篇文章的界面(之前我们用来重定向到介质页面)。

## 问题陈述

在我们发布后不久，我们在更新文章时遇到了一个问题，比如添加新内容、添加更多链接等等。问题陈述的分解—

*   每篇文章都存储在 Firebase 实时数据库中。
*   每篇文章都有一个名为 data 的键，用来存储文章的内容。
*   将来，在存储数据之后，我们只需要更新 article 对象的一个键，或者我们可能还需要更新数据。

这个怎么解决？

## 解决办法

首先，这个问题可以有多种解决方案，我们并不是说我们的解决方案是最好的。我们仍在学习，我真的相信每一次都有成长和提高的机会。

我们想到了一种方法，那就是使用 firebase 数据库对象提供的 set 方法。

## 什么是集合方法？

基本上，set 方法更新数据库中的值，如果值不存在，它就创建一个。但是 set 方法移除了对象中现有的键值。

## 警告

例如，您有一个包含两个键值对的对象，比如 email 和 password。在 firebase 中，只更新密码而不更改电子邮件有点混乱。如果您使用 set 方法并将更新后的密码传递给数据库，那么根据它的名称和解释，它应该只更新密码密钥，而不会涉及其他内容。

但是 set 方法与它完全相反，它删除了剩余的键，也就是我们例子中的 email，它将只创建/更新传递的键-值对。因此，如果您只传递密码，它将从对象中删除电子邮件密钥。

这就是为什么我把这个例子放在“注意”部分的原因😁因为我们曾经犯过这个错误，我希望这篇文章能帮助你。

## 如何最终更新值？

这有点简单，我们将只使用 set 方法，但是现在我们将把所有需要的键值对作为参数传递。因此，在我们的示例中，我们只需提供一个已经存储的电子邮件 id 和更新后的密码，并在 set 方法中传递这两个值。

我相信如果你有更好的解决方案，请在评论中告诉我们。

## 结论

我希望我们已经分享了这个故事所需要的意图。请继续关注更多这样的故事，并请订阅。

```
Our website - 💻 [iHateReading](http://ihatereading.in)
```

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*