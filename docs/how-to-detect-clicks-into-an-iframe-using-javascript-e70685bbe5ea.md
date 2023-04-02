# 如何使用 JavaScript 检测对 Iframe 的点击？

> 原文：<https://javascript.plainenglish.io/how-to-detect-clicks-into-an-iframe-using-javascript-e70685bbe5ea?source=collection_archive---------1----------------------->

![](img/407c530b90d5c46573a7f163c2b5ece2.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想检查用户是否使用 JavaScript 点击了 iframe。

在本文中，我们将看看如何用 JavaScript 检测对 iframe 的点击。

# 聚焦于主窗口，然后在窗口中添加一个模糊事件监听器

我们可以关注主窗口，然后在窗口中添加一个`blur`事件监听器，看看窗口发出`blur`事件后哪个元素被激活了。

例如，如果我们有以下 iframe:

```
<iframe src='https://example.com'></iframe>
```

然后我们可以把焦点放在窗口上，并通过编写以下代码向它添加一个`blur`监听器:

```
focus();
const listener = window.addEventListener('blur', () => {
  if (document.activeElement === document.querySelector('iframe')) {
    console.log('clicked on iframe')
  }
  window.removeEventListener('blur', listener);
});
```

我们调用`focus`来关注主窗口。

然后我们调用`window.addEventListener`向窗口添加一个`blur`事件监听器。

在事件监听器中，我们检查`document.activeElement`是否是 iframe，以检查 iframe 是否是我们关注的元素。

如果是，那么我们记录一条消息。

然后我们立即移除`blur`事件监听器。

现在，当我们单击 iframe 时，我们应该会看到记录的“clicked on iframe”消息。

# 结论

我们可以通过监听窗口上的`blur`事件来检测带有 JavaScript 的 iframe 中的点击。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。***