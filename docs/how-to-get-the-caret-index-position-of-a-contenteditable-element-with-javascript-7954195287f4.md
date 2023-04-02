# 如何用 JavaScript 获取 contentEditable 元素的插入符号索引位置

> 原文：<https://javascript.plainenglish.io/how-to-get-the-caret-index-position-of-a-contenteditable-element-with-javascript-7954195287f4?source=collection_archive---------6----------------------->

![](img/ffacf904fdf1d3cd40504c2730297715.png)

Photo by [Aditi Gautam](https://unsplash.com/@aditi_gautam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 获取一个`contentEditable`元素的插入符号索引位置。

在本文中，我们将看看如何用 JavaScript 获得一个`contentEditable`元素的插入符号索引位置。

# 使用 document.getSelector 方法

我们可以使用`document.getSelector`来获得选择。

然后我们可以用它来得到选择的长度，从而得到光标的位置。

例如，我们可以编写以下 HTML:

```
<div contenteditable>some text here <i>italic text here</i> some other text here <b>bold text here</b> end of text</div>
```

然后我们可以通过编写以下 JavaScript 代码来获取光标的位置:

```
const cursorPosition = () => {
  const sel = document.getSelection();
  sel.modify("extend", "backward", "paragraphboundary");
  const pos = sel.toString().length;
  if (sel.anchorNode != undefined) sel.collapseToEnd();
  return pos;
}const elm = document.querySelector('[contenteditable]');const printCaretPosition = () => {
  console.log(cursorPosition(), 'length:', elm.textContent.trim().length)
}
elm.addEventListener('click', printCaretPosition)
elm.addEventListener('keydown', printCaretPosition)
```

我们有`cursorPosition`函数，它调用`documebnt.getSelection`方法来获取 div 中的文本。

然后我们调用`modify`来调整当前选择。

我们通过`'paragraphboundary'`移动`'backward'`。

然后我们在将它转换成一个字符串后得到选择的长度。

然后我们折叠选择并返回`pos`来返回光标的位置。

接下来，我们用`querySelector`得到 div。

然后我们创建`printCaretPosition`来打印光标位置。

最后，我们调用`addEventListener`,这样当我们在 div 上点击或输入时，我们就调用`printCaretPosition`。

# 结论

我们可以使用`document.getSelector`来获得选择。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***