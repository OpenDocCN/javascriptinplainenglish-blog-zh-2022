# 如何使用 CSS 或 JavaScript 隐藏网页上的光标？

> 原文：<https://javascript.plainenglish.io/hoe-to-hide-the-cursor-in-a-webpage-using-css-or-javascript-6c744d2a0b0e?source=collection_archive---------1----------------------->

![](img/c25e24b022591985003f367417166218.png)

Photo by [Roxann Shepard](https://unsplash.com/@roxannshepard?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 CSS 或 JavaScript 隐藏网页上的光标。

在本文中，我们将看看如何使用 CSS 或 JavaScript 隐藏网页上的光标。

# 使用 CSS 隐藏网页中的光标

要用 CSS 隐藏网页上的光标，我们可以使用`cursor`属性。

例如，我们可以编写以下 HTML:

```
<div class="nocursor">
   Some stuff
</div>
```

然后，我们可以通过编写以下内容来隐藏鼠标在 div 中时的光标:

```
.nocursor {
  cursor: none;
}
```

# 使用 JavaScript 隐藏网页中的光标

要用 JavaScript 隐藏网页上的光标，我们可以使用`style.cursor`属性。

例如，我们可以编写以下 HTML:

```
<div class="nocursor">
   Some stuff
</div>
```

然后，我们可以通过编写以下内容来隐藏鼠标在 div 中时的光标:

```
document.getElementsByClassName('nocursor')[0].style.cursor = 'none';
```

我们用`getElementsByClassName`得到 div。

我们将它的`style.cursor`属性设置为`'none'`，当鼠标在 div 中时隐藏光标。

# 结论

要用 CSS 隐藏网页上的光标，我们可以使用`cursor`属性。

要用 JavaScript 隐藏网页上的光标，我们可以使用`style.cursor`属性。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。***