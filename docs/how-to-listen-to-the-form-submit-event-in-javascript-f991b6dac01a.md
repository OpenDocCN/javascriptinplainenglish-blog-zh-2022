# 如何在 JavaScript 中监听表单提交事件

> 原文：<https://javascript.plainenglish.io/how-to-listen-to-the-form-submit-event-in-javascript-f991b6dac01a?source=collection_archive---------1----------------------->

![](img/839ac291bbba9e9c3a516e491f35f96e.png)

Photo by [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 来监听表单提交事件，这样我们就可以在客户端对表单数据做一些事情。

在本文中，我们将看看如何用 JavaScript 监听表单提交事件。

# 监听提交事件

我们可以监听表单的`submit`事件来观察表单提交按钮的按下情况。

例如，如果我们有以下形式:

```
<form>
  <input type="text" name="name">
  <input type="submit" name="submit">
</form>
```

然后我们可以写:

```
const form = document.querySelector("form")
form.addEventListener("submit", (e) => {
  e.preventDefault();
  const formData = new FormData(form)
  console.log(formData.entries())
});
```

监听表单提交事件，并使用`FormData`构造函数从表单中获取数据。

我们用`document.querySelector`得到表格。

然后我们用`'submit'`作为第一个参数调用`addEventListener`。

`addEventListener`的第二个参数是一个回调函数，它在表单提交时处理表单。

在回调中，我们调用`e.preventDefault()`来停止服务器端的表单提交行为。

然后我们使用带有我们选择的`form`元素的`FormData`构造函数来获取它的值。

然后我们使用`entries`方法获得输入的值。

它返回带有表单值的键值对的迭代器。

每个条目的关键字是字段的`name`属性值。

而值就是值。

因此，如果我们在文本字段中输入“aaa ”,我们会得到:

```
[
  [
    "name",
    "aaa"
  ]
]
```

作为`entries`返回的结果。

# 结论

我们可以监听表单的`submit`事件来观察表单提交按钮的按下。

然后我们可以用`FormData`构造函数得到输入的值。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****