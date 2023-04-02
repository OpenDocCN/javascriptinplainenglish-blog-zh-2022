# 如何获取浏览器的滚动条大小？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-browsers-scrollbar-sizes-f6196f883096?source=collection_archive---------3----------------------->

![](img/fa4c08933172b439382fd424970182f9.png)

Photo by [Taylor Wilcox](https://unsplash.com/@taypaigey?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想得到一个元素的滚动条大小。

在本文中，我们将研究如何获取滚动条的大小，滚动条是可滚动元素的一部分。

# 使用 getBoundingClientRect 方法和 scrollHeight 属性

我们可以用元素的`getBoundingClientRect`方法和`scrollHeight`属性来获取元素的滚动条大小。

为此，我们用`scrollHeight`属性的值减去`getBoundingClientRect`方法返回的`height`属性值，得到水平滚动条的宽度。

例如，如果我们有:

```
<div id="app" style='width: 100px; overflow-x: scroll'></div>
```

然后，我们可以向 div 添加元素，并通过编写以下内容获得水平滚动条高度:

```
const app = document.querySelector('#app')
for (let i = 0; i < 100; i++) {
  const span = document.createElement('span')
  span.textContent = i
  app.appendChild(span)
}const getScrollbarHeight = (el) =>{
  return el.getBoundingClientRect().height - el.scrollHeight;
};
console.log(getScrollbarHeight(app))
```

我们用`querySelector`得到 div。

然后，我们在 div 中添加一些跨度。

div 设置了 width 和 overflow-x 来滚动。

这意味着 div 应该有一个水平滚动条。

接下来，我们创建`getScrollbarHeight`函数，用`scrollHeight`从`getBoundingClientRect`中减去`height`，得到水平滚动条的高度。

然后我们用控制台日志记录滚动条的高度。

同样，我们可以用以下公式得到滚动条宽度:

```
<div id="app" style='height: 100px; overflow-y: scroll'></div>
```

并且:

```
const app = document.querySelector('#app')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  app.appendChild(p)
}const getScrollbarHeight = (el) =>{
  return el.getBoundingClientRect().width - el.scrollWidth;
};
console.log(getScrollbarHeight(app))
```

我们将 p 元素添加到一个可垂直滚动的 div 中。

我们不是减去高度，而是减去宽度。

我们应该从控制台日志中得到滚动条的宽度。

# 结论

我们可以通过调用`getBoundingClientRect`方法得到滚动条的宽度和高度，并得到两者之间的差值。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*