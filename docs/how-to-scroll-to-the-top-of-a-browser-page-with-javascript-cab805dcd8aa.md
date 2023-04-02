# 如何用 JavaScript 滚动到浏览器页面顶部？

> 原文：<https://javascript.plainenglish.io/how-to-scroll-to-the-top-of-a-browser-page-with-javascript-cab805dcd8aa?source=collection_archive---------11----------------------->

## 如何使用 JavaScript 滚动到浏览器页面顶部的快速指南。

![](img/c5d89284074ddbdc9382f70d538270cb.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想用 JavaScript 滚动到浏览器页面的顶部。

在本文中，我们将看看如何用 JavaScript 滚动到浏览器页面的顶部。

# 使用 window.scrollTo 方法

我们可以使用`window.scrollTo`方法，将 x 和 y 坐标分别作为参数滚动到。

例如，如果我们有下面的 HTML:

```
<div></div>
<button>
  scroll to top
</button>
```

然后，我们可以编写以下 JavaScript 来将子元素添加到 div 中，并通过编写以下内容使按钮滚动到页面顶部:

```
const button = document.querySelector('button')
const div = document.querySelector('div')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}button.addEventListener('click', () => {
  window.scrollTo(0, 0);
})
```

我们用 for 循环来添加元素`document.createElement`。

然后我们将`textContent`设置为一些内容。

然后我们调用`appendChild`来添加元素。

接下来，我们用`'click'`调用`button.addEventListener`来添加一个点击监听器。

我们用 0 和 0 调用`scrollTo`来滚动到页面顶部。

因此，当我们点击“滚动到顶部”时，我们应该转到页面的顶部。

我们也可以用一个对象来改变滚动行为。

例如，我们可以写:

```
button.addEventListener('click', () => {
  window.scrollTo({
    top: 0,
    behavior: `smooth`
  })
})
```

`top`设置为 0 滚动到顶部。

`behavior`设置为`'smooth'`使滚动平滑。

# 结论

我们可以用`window.scrollTo`方法滚动到页面的顶部。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。****