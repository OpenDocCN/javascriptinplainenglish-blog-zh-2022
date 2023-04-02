# 如何用 JavaScript 处理右键点击？

> 原文：<https://javascript.plainenglish.io/how-to-handle-right-clicks-with-javascript-86d35714ce33?source=collection_archive---------1----------------------->

![](img/ccef3f2a594d0276fdc22b2c1f5ec1ae.png)

Photo by [Shane](https://unsplash.com/@theyshane?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，当用户右键单击我们的 web 应用程序中的元素时，我们想要做一些事情。

在本文中，我们将看看如何用 JavaScript 处理右键单击。

# 将 window.oncontextmenu 属性设置为函数

我们可以将`window.contextmenu`属性设置为一个事件处理函数来监听页面上的右键单击。

为此，我们写道:

```
window.oncontextmenu = (e) => {
  e.preventDefault()
  console.log('right clicked')
}
```

我们有包含右击事件对象的`e`参数。

我们调用`e.preventDefault`来停止右击的默认行为，即在页面上显示上下文菜单。

一旦我们调用了这个函数，当用户右击页面时，我们可以在函数的其余部分做任何我们想做的事情。

# 调用 window.addEventListener 方法添加事件侦听器函数

当我们右击页面时，另一种方法是调用`window.addEventListener`方法来添加一个事件监听器函数来监听右击。

例如，我们可以写:

```
window.addEventListener('contextmenu', (ev) => {
  ev.preventDefault();
  console.log('right clicked')
});
```

我们传入`'contextmenu'`字符串来监听上下文菜单的点击事件。

然后在事件监听器中，我们用同样的方法调用`preventDefault`来停止显示默认的右键菜单。

然后当用户右击页面时，我们可以做我们想做的事情。

# 结论

我们可以监听`contextmenu`事件，并在右键单击页面时调用事件处理函数中的`preventDefault`来运行我们自己的 JavaScript。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***