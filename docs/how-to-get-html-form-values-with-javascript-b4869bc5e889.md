# 如何用 JavaScript 获取 HTML 表单值

> 原文：<https://javascript.plainenglish.io/how-to-get-html-form-values-with-javascript-b4869bc5e889?source=collection_archive---------0----------------------->

## 用 JavaScript 获取 HTML 表单值的教程

![](img/c9ed190db4162bfc15f415419ba4528e.png)

Photo by [Andy Art](https://unsplash.com/@trojantry?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 获取 HTML 表单值。

在本文中，我们将研究如何用 JavaScript 获取 HTML 表单值。

# 使用 FormData 构造函数

我们可以使用`FormData`构造函数创建一个对象，获取我们输入的表单值的键值对。

例如，如果我们有以下形式:

```
<form>
  Credit Card Validation:
  <input type="text" name="cctextbox">
  <br /> Card Type:
  <select name="cardtype">
    <option value="visa">Visa</option>
    <option value="mastercard">MasterCard</option>
    <option value="discover">Discover</option>
    <option value="amex">Amex</option>
    <option value="diners">Diners Club</option>
  </select>
  <br />
  <input type="submit" />
</form>
```

然后我们可以写:

```
const form = document.querySelector('form')
form.addEventListener('submit', (e) => {
  e.preventDefault()
  const formData = new FormData(form)
  for (const pair of formData.entries()) {
    console.log(pair)
  }
})
```

侦听表单的提交事件，并在提交时获取值。

我们首先用`document.querySelector`获取表单元素。

然后我们调用`addEventListener`将提交事件监听器添加到表单中。

`addEventListener`的第二个参数是提交事件监听器。

我们调用`e.preventDefault`来防止默认提交行为，这样我们就可以进行客户端表单提交。

然后我们用`FormData`构造函数创建`formData`对象，用`form`作为参数来获取表单数据值。

然后我们调用`formData.entries`来获得表单数据密钥对对的数组。

那么`pair`应该是这样的:

```
["cctextbox", "aa"]
["cardtype", "visa"]
```

其中第一个条目是`name`属性值，第二个条目是输入值。

# 结论

我们可以获得用`FormData`构造函数输入的表单值。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***