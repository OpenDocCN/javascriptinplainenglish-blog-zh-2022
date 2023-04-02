# 如何确定 HTML 元素的内容是否溢出了 JavaScript

> 原文：<https://javascript.plainenglish.io/how-to-determine-if-an-html-elements-content-overflows-with-javascript-85ce5bceef14?source=collection_archive---------1----------------------->

## 使用 JavaScript 判断 HTML 元素内容是否溢出的教程。

![](img/8d8df9b25d7a9b9cac8a28b5cea03d6a.png)

Photo by [Adrian Swancar](https://unsplash.com/@a_d_s_w?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想确定 HTML 元素的内容是否溢出了 JavaScript。

在本文中，我们将看看如何确定 HTML 元素的内容是否溢出了 JavaScript。

# 检查 scrollWidth 和 scrollHeight 是否分别大于 clientWidth 和 clientHeight

HTML 元素的`scrollWidth`属性具有元素内容的全宽度。

HTML 元素的`scrollHeight`属性具有元素中内容的完整高度。

HTML 元素的`clientWidth`属性具有元素中所显示内容的宽度。

HTML 元素的`clientHeight`属性具有所显示元素中内容的高度。

因此，我们可以对它们进行比较，看是否有内容溢出。

如果`scrollWidth`大于`clientWidth`或者`scrollHeight`大于`clientHeight`，那么我们知道内容溢出了。

例如，如果我们有下面的 HTML:

```
<div style='width: 100px; height: 100px; overflow: auto'>
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer efficitur mauris at nisl accumsan suscipit. Aliquam tempus ultrices consectetur.
</div>
```

然后，我们可以通过编写以下代码来检查 div 的内容是否溢出了 div:

```
const checkOverflow = (el) => {
  const isOverflowing = el.clientWidth < el.scrollWidth ||
    el.clientHeight < el.scrollHeight;
  return isOverflowing;
}const div = document.querySelector('div')
console.log(checkOverflow(div))
```

我们创建了将`el` DOM 元素对象作为参数的`checkOverflow`函数。

并返回我们描述的`clientWidth`和`scrollWidth`以及`clientHeight`和`scrollHeight`之间的比较。

控制台日志应该记录`true`，因为 div 中的文本溢出了 div 的高度，所以`el.clientHeight < el.scrollHeight`返回`true`。

# 结论

如果`scrollWidth`大于`clientWidth`或者`scrollHeight`大于`clientHeight`，那么我们知道内容溢出。

所以我们可以用这个事实来检查 DOM 元素的内容是否溢出了 JavaScript。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***