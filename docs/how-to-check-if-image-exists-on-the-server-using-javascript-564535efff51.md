# 如何使用 JavaScript 检查图像是否存在于服务器上

> 原文：<https://javascript.plainenglish.io/how-to-check-if-image-exists-on-the-server-using-javascript-564535efff51?source=collection_archive---------0----------------------->

## 关于如何用 JavaScript 检查服务器上是否存在图像的教程。

![](img/4a29008e2a8db96b24302772e5e2226a.png)

Photo by [Jocelyne Yvonne](https://unsplash.com/@ledi777?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 检查服务器上是否存在图像。

在本文中，我们将看看如何用 JavaScript 检查服务器上是否存在图像。

# 听取图像错误事件

当图像加载失败时，我们可以监听由图像元素触发的错误事件，以检查从服务器加载图像时是否触发了任何错误。

例如，我们可以写:

```
const image = new Image();image.onload = () => {
  document.body.appendChild(image);
}
image.onerror = () => {
  const err = new Image();
  err.src = 'https://i.picsum.photos/id/918/200/300.jpg?hmac=1gEvFp6O-XDh4848VnlwyOIrVy8s_aJNhYyTzxN9_JA';
  document.body.appendChild(err);
}image.src = "abc";
```

我们使用`Image`构造函数来创建一个图像 DOM 元素对象。

然后，我们将`img.onload`属性设置为一个在图像成功加载时运行的函数。

在函数中，我们调用`document.body.appendChild`将图像添加到 body 元素中。

接下来，我们将`img.onerror`属性设置为在原始图像加载失败时运行的函数。

在这个函数中，我们创建了一个新的`Image`实例，并将`src`设置为我们加载的图像，以防原始图像加载失败。

最后，我们将`image.src`设置为一个无效的 URL，这样`onerror`方法就会运行并加载回退图像。

# 结论

我们可以监听图像的`error`事件，看看我们加载的原始图像何时加载失败。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***