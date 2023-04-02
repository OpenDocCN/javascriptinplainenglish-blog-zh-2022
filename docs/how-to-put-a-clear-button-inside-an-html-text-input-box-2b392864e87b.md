# 如何在 HTML 文本输入框中放置一个清除按钮？

> 原文：<https://javascript.plainenglish.io/how-to-put-a-clear-button-inside-an-html-text-input-box-2b392864e87b?source=collection_archive---------1----------------------->

![](img/25addc5d21248d7f17cfe21c667a93d7.png)

Photo by [Devon Janse van Rensburg](https://unsplash.com/@devano23?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想在 HTML 文本输入框中添加一个清除按钮。

在本文中，我们将看看如何用 JavaScript 在 HTML 输入文本框中放置一个清除按钮。

# 添加带有搜索类型的输入元素

添加带有清除按钮的输入框的最简单方法是添加一个`input`元素，并将`type`属性设置为`search`。

例如，我们可以写:

```
<input type="search" />
```

然后，当我们在输入框中输入内容时，我们会看到 clear 按钮显示出来。

我们可以点击它来清除它的值。

# 使用 CSS 样式

我们也可以用 CSS 添加一个输入框。

例如，我们可以写:

```
<form>
  <input type="text" placeholder=" " />
  <button type="reset">&times;</button>
</form>
```

然后，我们可以对输入进行样式化，添加一个清除按钮:

```
form {
  position: relative;
  width: 200px;
}form input {
  width: 100%;
  padding-right: 20px;
  box-sizing: border-box;
}form input:placeholder-shown+button {
  opacity: 0;
  pointer-events: none;
}form button {
  position: absolute;
  border: none;
  display: block;
  width: 15px;
  height: 15px;
  line-height: 16px;
  font-size: 12px;
  border-radius: 50%;
  top: 0;
  bottom: 0;
  right: 5px;
  margin: auto;
  background: #ddd;
  padding: 0;
  outline: none;
  cursor: pointer;
  transition: .1s;
}
```

我们用`form button`选择器选择 CSS 表单中的按钮。

我们将它的`position`设置为`absolute`以使按钮保持在原位。

然后我们设置宽度和高度来适应输入框。

我们还设置了`background`来添加背景。

为了在按钮中添加“x ”,我们使用了`&times` HTML 实体。

按钮应该有`reset`作为`type`属性的值，以便在我们单击它时清除按钮的值。

# 结论

添加带有清除按钮的输入框的最简单方法是添加一个`input`元素，将`type`属性设置为`search`。

我们也可以在自己的按钮上添加自己的 CSS，来添加一个按钮来清除表单输入。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****