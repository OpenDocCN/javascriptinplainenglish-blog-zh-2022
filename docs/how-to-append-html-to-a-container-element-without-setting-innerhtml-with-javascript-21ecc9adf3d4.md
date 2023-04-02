# 如何在不使用 JavaScript 设置 innerHTML 的情况下将 HTML 追加到容器元素中？

> 原文：<https://javascript.plainenglish.io/how-to-append-html-to-a-container-element-without-setting-innerhtml-with-javascript-21ecc9adf3d4?source=collection_archive---------7----------------------->

![](img/7427e6efcaebca790020ac5be4b4d60d.png)

Photo by [Macau Photo Agency](https://unsplash.com/@macauphotoagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

通常，我们希望将 HTML 内容添加到容器元素中。

有时，我们想在不设置容器元素的`innerHTML`属性的情况下这样做。

在本文中，我们将了解如何在不使用 JavaScript 设置容器元素的`innerHTML`属性的情况下将 HTML 附加到容器元素中。

# 使用 document.createElement 和 appendChild

向容器元素添加子元素而不设置`innerHTML`属性的一种方法是使用`document.createElement`方法来创建元素。

然后我们可以调用`appendChild`来追加元素。

例如，如果我们有下面的 HTML:

```
<div></div>
```

然后我们可以写:

```
const element = document.querySelector('div')
const e = document.createElement('div');
const htmldata = 'hello world'
e.innerHTML = htmldata;while (e.firstChild) {
  element.appendChild(e.firstChild);
}
```

我们得到用`querySelector`添加的 div。

然后我们调用`document.createElement`来创建另一个 div，我们将它作为子元素插入到父 div 中。

我们设置新创建的元素的`e.innerHTML`的值，向其中添加一些内容。

然后我们调用`element.appendChild`将子元素添加到我们最初添加的 div 中。

现在我们应该在屏幕上看到“你好，世界”。

# 使用 insertAdjacentHTML 方法

将子元素作为子元素插入容器元素的另一种方法是使用`insertAdjacentHTML` 方法。

如果我们有下面的 HTML:

```
<div></div>
```

然后我们可以通过写来使用它:

```
const element = document.querySelector('div')
element.insertAdjacentHTML('beforeend', '<div>hello world</div>');
```

我们用`querySelector`得到 div。

然后我们用`'beforeend'`和我们想要插入 div 的 HTML 作为参数调用`insertAdjacentHTML`。

现在我们应该看到与上一个例子相同的结果。

# 结论

我们可以通过使用 DOM element 对象中可用的各种方法将 HTML 附加到容器元素中，而无需用 JavaScript 设置 innerHTML。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*