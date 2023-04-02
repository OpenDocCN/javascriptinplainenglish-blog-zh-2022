# 在 JavaScript 中将方法作为事件处理程序传递的正确方式

> 原文：<https://javascript.plainenglish.io/the-correct-way-to-pass-methods-as-event-handlers-in-javascript-f8aff0e228a4?source=collection_archive---------13----------------------->

## 那些括号会产生很大的差别并改变结果

![](img/23a2c76acdc62a3550c7a0de9b4aea4f.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@altumcode?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

前几天，我的一个同事在 JS 方法中没有收到预期的参数。他正在**尝试**让一个第三方 Vue.js 插件在一个项目中工作(就像我们所有人在信心波动时所做的那样)。

让我们看一个简单的普通 Javascript 例子，但是这个规则适用于任何地方(包括你最喜欢的 JS 框架)。

```
document.getElementById("just-do-it").addEventListener("click", spreadHappiness());

function spreadHappiness() {
    console.log('You are awesome');
}
```

你认为当用户点击那个按钮时会发生什么？

猜对了？

没什么！

![](img/ba3c100e2c0ccfa8be216a9c821a545f.png)

该方法在页面加载时被调用，单击按钮时不会发生任何事情。嗯…

你有没有注意到我们在第一行的方法名`spreadHappiness()`后面加了括号`()`？

这是典型的*引用调用*对*值调用*的事情。

那一行应该这样写(去掉括号):

```
document.getElementById("just-do-it").addEventListener("click", spreadHappiness);
```

这样，单击该按钮就会像预期的那样在浏览器控制台中记录该语句。

现在，您知道事件处理程序接收一个基于[事件](https://developer.mozilla.org/en-US/docs/Web/API/Event)接口的对象作为参数吗？这意味着您可以在您的方法中使用事件元数据。像这样:

```
function spreadHappiness(event) {
    console.log(event.type); // click
}
```

因此，在大多数情况下，当将方法名作为事件处理程序传递时，应该跳过这些括号。当需要动态获取事件处理程序时，调用另一个方法并返回它是有意义的。

# 关闭

简而言之，在指定事件处理程序**时，在方法名后面加上括号并不是一件可选的事情。它改变了结果。**

method(): *立即执行，返回值用作事件处理程序。*

方法:*用作事件处理程序，它在被调用时接收参数。*

同样，*进行方法调用*和*传递方法引用*是两回事，开发者，尤其是初学者，应该意识到这种区别。

你的朋友需要知道这些吗？把这篇文章分享给他们，让他们的调试生活更轻松。

*原载于*[*https://blog . fresh bits . in*](https://blog.freshbits.in/the-correct-way-to-pass-methods-as-event-handlers-in-javascript)*。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**