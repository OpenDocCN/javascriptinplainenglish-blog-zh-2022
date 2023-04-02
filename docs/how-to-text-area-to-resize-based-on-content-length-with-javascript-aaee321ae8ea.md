# 如何用 JavaScript 让文本区域根据内容长度调整大小

> 原文：<https://javascript.plainenglish.io/how-to-text-area-to-resize-based-on-content-length-with-javascript-aaee321ae8ea?source=collection_archive---------8----------------------->

## 一个关于使用 JavaScript 调整文本区域大小以包含所有内容的教程。

![](img/3da33974f75ca5aa1382600af1fab93f.png)

Photo by [Hogr Othman](https://unsplash.com/@hogrothman?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望调整文本区域的大小，以便用 JavaScript 将所有内容包含在内。

在本文中，我们将研究如何用 JavaScript 调整文本区域的大小，以包含其中的所有内容。

# 将文本区域的高度设置为滚动高度

文本区域元素的`scrollHeight`属性具有以像素为单位的内容的完整高度。

因此，我们只需要将文本区域的高度设置为滚动高度，就可以将文本区域的高度设置为环绕文本区域的所有内容。

例如，如果我们有下面的 HTML:

```
<textarea></textarea>
```

然后我们可以得到文本区域，然后通过编写以下内容将高度设置为滚动高度:

```
const textarea = document.querySelector('textarea')
textarea.addEventListener('keyup', () => {
  textarea.style.height = `${textarea.scrollHeight}px`;
})
```

我们用`document.querySelector`得到文本区域。

然后我们调用`addEventListener`，用`'keyup'`作为第一个参数，为文本区域添加一个 keyup 监听器。

在事件监听器中，我们将`style.height`设置为`textarea.scrollHeight`，以将文本区域的高度设置为内部内容的高度。

我们应该记得包括单位，以便设置高度。

现在，当我们在文本区域中键入内容时，它会调整高度以环绕所有内容。

# 结论

我们可以将文本区域的高度设置为滚动高度，以设置文本区域的高度来环绕文本区域的所有内容。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***