# 如何用 JavaScript 滚动回可滚动 Div 的顶部

> 原文：<https://javascript.plainenglish.io/how-to-scroll-back-to-the-top-of-a-scrollable-div-with-javascript-e3e8ff690011?source=collection_archive---------3----------------------->

## 用 JavaScript 滚动回可滚动 div 顶部的教程。

![](img/40fdb1d7bb688fafb54f2d6ceec3c81e.png)

Photo by [Taylor Wilcox](https://unsplash.com/@taypaigey?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 滚动回一个可滚动的 div 的顶部。

在本文中，我们将研究如何用 JavaScript 滚动回可滚动 div 的顶部。

# 使用滚动方法

我们可以使用元素的`scroll`方法将一个可滚动的 div 滚动回顶部。

例如，如果我们有下面的 HTML:

```
<button>
  scroll to top
</button>
<div></div>
```

和下面的 CSS:

```
div {
  height: 300px;
  overflow-y: scroll;
}
```

然后，我们可以向 div 添加一些内容，并通过编写以下代码使 div 在我们单击按钮时滚动到顶部:

```
const div = document.querySelector('div')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}const btn = document.querySelector('button')
btn.addEventListener('click', () => {
  div.scroll({
    top: 0,
    behavior: 'smooth'
  });
});
```

我们用`document.querySelector`得到 div。

然后我们添加一个 for 循环，用`document.createElement`向 div 添加一些内容，创建一个 p 元素。

我们调用`div.appendChild`将 p 元素添加到 div 中。

接下来，我们得到带有`document.querySelector`的按钮。

然后我们调用按钮上的`addEventListener`来添加一个点击监听器。

在 click listener 中，我们用一个对象调用`div.scroll`并将`top`设置为 0 来滚动到顶部。

并且`behavior`被设置为`'smooth'`以增加平滑滚动。

现在，当我们单击“滚动到顶部”按钮时，可滚动的 div 应该在滚动过程中以平滑的滚动运动回到顶部。

# 结论

我们可以使用`scroll`方法将一个 div 滚动到顶部。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***