# 如何在 DOM 中添加一个 JavaScript 字符串？

> 原文：<https://javascript.plainenglish.io/how-to-append-a-javascript-string-to-the-dom-e936a6a888c1?source=collection_archive---------4----------------------->

![](img/396791560fb7a698c18d33f9053a8520.png)

Photo by [Sarra Marzguioui](https://unsplash.com/@geist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 在元素的 HTML 内容中追加一个字符串。

在本文中，我们将研究如何用 JavaScript 将字符串追加到元素的 HTML 内容中。

# 使用 DOM 节点的 appendChild 方法

我们可以在一个 DOM 节点上调用`appendChild`,将一个子节点附加到给定的 DOM 节点上。

例如，如果我们有给定的 div:

```
<div id='test'>
  foo
</div>
```

然后我们可以添加另一个 div 作为上面 div 的子 div，并添加`appendChild`。

为此，我们写道:

```
const child = document.createElement('div');
child.innerHTML = 'bar';
const {
  firstChild
} = child;
document.getElementById('test').appendChild(firstChild);
```

我们调用`documenbt.createElement`来创建`child` div 元素。

然后我们将它的`innerHTML`设置为 div 中我们想要的内容。

接下来，我们从`child`得到`firstChild`。

然后我们用`firstChild`调用 ID 为`test`的 div 上的`appendChild`，将它附加为 ID 为`test`的 div 的另一个子节点。

现在我们看到显示“foo bar”。

# 向 innerHTML 值追加一个字符串

我们也可以直接在`innerHTML`后面添加一个字符串。

所以如果我们有:

```
<div id='test'>
  foo
</div>
```

然后我们可以使用`+=`操作符将一个字符串添加到 ID 为`test`的 div 中，方法是:

```
document.getElementById('test').innerHTML += ' bar'
```

我们得到了和上一个例子一样的结果。

# 结论

我们可以在一个 DOM 节点上调用`appendChild`,将一个子节点附加到一个给定的 DOM 节点上。

我们也可以直接在`innerHTML`后面添加一个字符串。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费周报**](http://newsletter.plainenglish.io/) 。关注我们 [**推特**](https://twitter.com/inPlainEngHQ) ，[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**，**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**，以及** [**不和谐**](https://discord.gg/GtDtUAvyhW) **。**

## 想用内容来扩展你的科技创业吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。