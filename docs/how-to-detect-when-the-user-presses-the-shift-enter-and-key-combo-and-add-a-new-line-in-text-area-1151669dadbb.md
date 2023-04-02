# 如何检测用户何时按下 Shift+Enter 和组合键，并在用户这样做时在文本区域添加一个新行？

> 原文：<https://javascript.plainenglish.io/how-to-detect-when-the-user-presses-the-shift-enter-and-key-combo-and-add-a-new-line-in-text-area-1151669dadbb?source=collection_archive---------16----------------------->

![](img/597298954b2ca1024b9f9c3fc313f36a.png)

Photo by [Marita Kavelashvili](https://unsplash.com/@maritafox?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望检测用户何时按下 shift-enter 组合键，并在用户这样做时在文本区域添加一个新行。

在本文中，我们将研究如何在光标位于文本区域时检测按下的 shift-enter 组合键。

# 在文本区域添加文本选择以移动光标

我们可以通过在文本区域中添加一个选择范围，将文本区域中的光标移动到下一行。

例如，如果我们有以下文本区域:

```
<textarea></textarea>
```

然后我们可以监听`keydown`事件来检测 shift+enter 组合键的按下。

如果组合被按下，那么我们停止默认行为，然后将文本选择添加到文本区域，将光标移动到下一行。

为此，我们写道:

```
const pasteIntoInput = (el, text) => {
  el.focus();
  if (typeof el.selectionStart === "number" &&
    typeof el.selectionEnd === "number") {
    const val = el.value;
    const selStart = el.selectionStart;
    el.value = val.slice(0, selStart) + text + val.slice(el.selectionEnd);
    el.selectionEnd = el.selectionStart = selStart + text.length;
  } else if (typeof document.selection !== "undefined") {
    const textRange = document.selection.createRange();
    textRange.text = text;
    textRange.collapse(false);
    textRange.select();
  }
}const handleEnter = (evt) => {
  if (evt.keyCode === 13 && evt.shiftKey) {
    if (evt.type === "keypress") {
      evt.preventDefault();
      pasteIntoInput(evt.target, "\n");
    }
  }
}const textarea = document.querySelector('textarea')
textarea.addEventListener('keydown', handleEnter)
```

我们有接受`el`元素和`text`值的`pasteIntoInput`函数。

在函数中，我们调用`el.focus`来关注元素。

然后我们检查`selectionStart`和`selectionEnd`是否是一个数。

然后，我们将`el.value`设置为选择文本的第一部分，将它与`text`连接，并将它与所选文本的第二部分连接。

然后我们将`el.selectionEnd`设置为文本的新长度。

如果`documebt.selection`是`undefined`，

然后我们用`documenbt.selection.createRange`创建一个新的选择。

然后我们设置选择的文本，所有的`collapse`折叠选择并调用`select`选择它。

接下来，我们创建`handleEnter`函数，它是事件处理程序。

我们检测 shift+enter 组合键并停止默认行为，如果组合键被按下，调用`pasteIntoInput`在文本区域粘贴一个新行。

最后，我们用`querySelector`选择文本区域。

然后我们调用`addEventListener`来监听文本区域上的`keydown`事件。

现在，当我们按 shift+enter 时，光标将移动到新的一行。

# 结论

我们可以通过停止默认行为，在按下 shift+enter 时在文本区域插入一个新行，然后在选中的文本中添加一个新行字符，并将其设置为文本区域的新`value`来添加新行。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***