# 如何检查一张背景图片是否加载了 JavaScript？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-background-image-is-loaded-with-javascript-32088a0d1f1e?source=collection_archive---------3----------------------->

## 如何用 JavaScript 检查页面上是否加载了背景图片的指南。

![](img/b16227bbf4c10ba0e778422159dfd641.png)

Photo by [Ball Park Brand](https://unsplash.com/@ballparkbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想检查背景图片是否加载了 JavaScript。

在本文中，我们将看看如何用 JavaScript 检查页面上是否加载了背景图像。

# 侦听加载事件

我们可以监听一个背景图片的`load`事件，看看它是否被加载。

如果它被加载，那么我们可以将背景图像设置为与背景图像具有相同 URL 的图像。

例如，我们可以写:

```
const imageUrl = "https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png";
const bgElement = document.querySelector("body");
let preloaderImg = document.createElement("img");
preloaderImg.src = imageUrl;preloaderImg.addEventListener('load', (event) => {
  bgElement.style.backgroundImage = `url(${imageUrl})`;
  preloaderImg = null;
});
```

我们有一个`imageUrl`,它包含了我们想要作为背景图片加载的图片。

然后我们用`document.querySelector`得到主体元素。

然后我们用我们想要预加载的图像创建带有`document.createElement`的`preloaderImg`元素。

接下来，我们将`preloaderImg.src`设置为`imageUrl`。

然后我们调用`preloaderImg`上的`addEventListener`，用`'load'`作为第一个参数来观察`preloaderImg`的加载。

回调将在加载后运行。

因此，我们可以设置`bgElement.style.backgroundImage`来将背景图像设置为加载到`preloaderImg`元素中的图像。

然后我们将`preloaderImg`设置为`null`来清除预加载的图像。

现在，我们应该看到页面上加载的背景图像。

# 结论

我们可以监听一个图像元素的`load`事件，看看是否加载了一个图像。

然后一旦它被加载，我们就可以使用预加载图像的图像 URL 来设置页面的背景图像。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*