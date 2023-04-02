# JavaScript:如何添加和删除事件监听器

> 原文：<https://javascript.plainenglish.io/javascript-how-to-add-and-remove-event-listeners-a9a67ca6dce0?source=collection_archive---------2----------------------->

## 事件侦听器的目的是什么？事件侦听器确保您的页面在特定操作发生时做出相应的响应。

![](img/f2a4e68c6354125c4167a7c06f953ec2.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这篇博文中，我们将讨论如何在 JavaScript 中添加和删除事件监听器。事件侦听器对于处理网站上的用户交互非常重要。通过添加事件侦听器，您可以确保当特定操作发生时，您的页面会做出相应的响应。

## 什么是事件监听器？

事件监听器是在事件发生时触发的功能。例如，如果您的页面上有一个按钮，并且您希望当用户单击该按钮时发生一些事情，那么您可以为“click”事件添加一个事件侦听器。该按钮将监听“点击”事件，并在该事件发生时执行一个功能。

## 添加事件侦听器

可以使用 addEventListener()方法将事件侦听器添加到元素中。这个方法有两个参数:您正在监听的事件，以及事件发生时应该执行的函数。可以在 HTML 元素的任何元素上调用 addEventListener()方法。例如，如果我们想在按钮上添加一个点击监听器，我们可以这样做:

```
button.addEventListener(“click”, myFunction);
```

在这段代码中，我们为“click”事件添加了一个侦听器。当“click”事件发生时，我们的 myFunction 将被执行。

示例中的 myFunction 是第二个参数(回调函数)的占位符。你可以随意命名你的回调函数。

您可以为许多不同的事件添加侦听器。一些常见事件包括:

*   点击
*   鼠标悬停
*   按键

您可以在 Mozilla 开发者网络网站上找到完整的活动列表。

一旦添加了事件侦听器，它将侦听指定事件的发生。当该事件发生时，您的函数将被执行。

![](img/256af3201799b1d18ca2a554311fd6f5.png)

Photo by [Emile Perron](https://unsplash.com/@emilep?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 删除事件侦听器

您可以使用 removeEventListener()方法移除事件侦听器。该方法采用相同的两个参数:要移除的事件类型，以及该事件发生时应该执行的回调函数。removeEventListener()方法可以在 HTML 元素的任何元素上调用。

例如，如果我们想从按钮中删除我们的点击监听器，我们将执行以下操作:

```
button.removeEventListener(“click”, myFunction);
```

在这段代码中，我们删除了之前添加的“click”事件侦听器。一旦删除了事件侦听器，它将不再侦听指定事件的发生。当该事件发生时，您的函数将不会被执行。

## 为什么事件侦听器有用

事件侦听器非常有用，因为它们允许您对网站上的用户交互做出响应。通过添加事件侦听器，您可以使您的网站更具交互性和响应性。

例如，您可以使用事件侦听器来:

*   当用户单击按钮时显示弹出窗口
*   当用户按 enter 键时提交表单
*   当用户滚动到页面底部时加载新内容

## 结论

这些只是几个如何使用事件侦听器的例子。事件侦听器是一个强大的工具，您可以使用它来为您的网站添加交互式功能。

我希望你能从这篇文章中学到一些东西。祝你的项目好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***