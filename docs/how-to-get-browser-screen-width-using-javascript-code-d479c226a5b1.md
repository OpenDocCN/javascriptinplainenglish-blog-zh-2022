# 如何用 JavaScript 代码获取浏览器屏幕宽度？

> 原文：<https://javascript.plainenglish.io/how-to-get-browser-screen-width-using-javascript-code-d479c226a5b1?source=collection_archive---------18----------------------->

![](img/273c46e61272588699d99d2dff8dbe8c.png)

Photo by [Panos Sakalakis](https://unsplash.com/@meymigrou?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 代码获得浏览器屏幕的宽度。

在本文中，我们将看看如何用 JavaScript 代码获得浏览器屏幕的宽度。

# 使用 document.body 或 document.documentElement 的属性

`document.body`是 HTML body 元素的 JavaScript 版本。

`document.documentElement`是 HTML `html` 元素的 JavaScript 版本。

我们需要它的属性来获得浏览器屏幕的宽度。

例如，我们可以写:

```
const getWidth = () => {
  return Math.max(
    document.body.scrollWidth,
    document.documentElement.scrollWidth,
    document.body.offsetWidth,
    document.documentElement.offsetWidth,
    document.documentElement.clientWidth
  );
}console.log(getWidth())
```

创建一个函数来获取浏览器屏幕的宽度。

`document.body.scrollWidth`是`body`元素内容的全角。

`document.documentElement.scrollWidth`是`html`元素内容的全宽。

`document.body.offsetWidth`是`body`元素的宽度，包括任何边框、填充和垂直滚动条。

`document.documentElement.offsetWidth`是`html`元素的宽度，包括任何边框、填充和垂直滚动条。

`document.documentElement.clientWidth`是以像素为单位的元素的内部宽度。它包括填充，但不包括`html`元素的边框、边距和垂直滚动条。

每一个都是以像素为单位。

因此，我们可以使用`Math.max`方法来获取它们之间的最大值。

该函数应该返回所有这些值之间的最大值。

# 结论

我们可以使用`document.body`或`document.documentElement`的各种属性来获得屏幕的宽度。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*