# 如何用 JavaScript 观察鼠标滚轮事件

> 原文：<https://javascript.plainenglish.io/how-to-watch-for-mouse-wheel-events-with-javascript-1cc8b5ac4730?source=collection_archive---------4----------------------->

## 通过监听`wheel`事件，用 JavaScript 观察鼠标滚轮事件。

![](img/edf8cc68d6c4de231c36c125160afaea.png)

Photo by [Ryan Stone](https://unsplash.com/@rstone_design?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，当用户在我们的 web 应用程序中移动鼠标滚轮时，我们想要做一些事情。

在本文中，我们将看看如何用 JavaScript 来观察鼠标滚轮事件。

# 用 JavaScript 观察鼠标滚轮事件

我们可以通过监听`wheel`事件来用 JavaScript 观察鼠标滚轮事件。

例如，我们可以写:

```
let supportOffset = window.pageYOffset !== undefined,
  lastKnownPos = 0,
  scrollDir,
  currYPos;
window.addEventListener('wheel', (e) => {
  currYPos = supportOffset ? window.pageYOffset : document.body.scrollTop;
  scrollDir = lastKnownPos > currYPos ? 'up' : 'down';
  lastKnownPos = currYPos;
  console.log(lastKnownPos, currYPos, scrollDir)
});
```

调用`window.addEventListener`来观察浏览器标签上的鼠标滚轮运动。

在事件处理程序回调中，我们将`currYPos`设置为`window.pageYOffset`或`document.body.scrollTop`以获取垂直滚动条的当前位置。

然后我们对照`currYPos`的前一个值`lastKnownPos`进行检查。

如果`lastKnownPos > currYPos`是`true`，那么我们向上滚动，因为当前位置的像素小于`lastKnownPos`。

否则，我们将向下滚动。

现在，当我们上下滚动具有可滚动内容的浏览器选项卡时，我们应该会看到控制台日志中记录的值。

# 结论

我们可以通过 JavaScript 监听`wheel`事件来监听鼠标滚轮事件。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***