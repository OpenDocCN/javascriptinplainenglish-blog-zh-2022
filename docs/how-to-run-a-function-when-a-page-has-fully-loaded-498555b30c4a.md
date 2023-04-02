# 当一个页面已经完全加载时，如何运行一个函数？

> 原文：<https://javascript.plainenglish.io/how-to-run-a-function-when-a-page-has-fully-loaded-498555b30c4a?source=collection_archive---------10----------------------->

![](img/b68842605080dbc9f6c025e2c9f3ee98.png)

Photo by [Kym MacKinnon](https://unsplash.com/@vixenly?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在网页满载时运行一些代码。

在本文中，我们将研究如何在页面完全加载 JavaScript 时运行一个函数。

# 侦听加载事件

当页面完全加载时，触发`load`事件。

因此，我们可以通过给它附加一个事件处理函数来监听`load`事件，以便在页面完全加载时运行代码。

例如，我们可以写:

```
window.addEventListener('load', () => {
  console.log("page is loaded")
})
```

我们调用`window.addEventListener`来监听页面上触发的`load`事件。

在第二个参数中，我们传入一个回调函数，该函数在`load`事件被触发时运行。

因此，当网页被加载时，我们应该看到`'page is loaded'`被记录。

# 侦听 DOMContentLoaded 事件

同样，我们可以监听页面完全加载时触发的`DOMContentLoaded`事件。

所以我们可以像处理`load`事件一样，给它附加一个事件处理程序。

例如，我们可以写:

```
window.addEventListener('DOMContentLoaded', () => {
  console.log("page is loaded")
})
```

当页面完全加载时，在第二个参数中运行回调。

因此，当网页被加载时，我们应该看到记录的`'page is loaded'`。

# 设置 window.onload 方法

我们可以将`window.onload`方法设置为我们希望在页面完全加载时运行代码的函数。

这是因为`window.onload`在页面完全加载时运行。

为此，我们写道:

```
window.onload = () => {
  console.log("page is loaded")
}
```

我们只是将`onload`属性设置为一个我们希望在页面加载时运行的函数。

因此，我们应该看到在加载网页时记录的`'page is loaded'`。

# 结论

当网页完全加载了 JavaScript 时，我们可以使用几种方法来运行函数。

*更多内容请看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***