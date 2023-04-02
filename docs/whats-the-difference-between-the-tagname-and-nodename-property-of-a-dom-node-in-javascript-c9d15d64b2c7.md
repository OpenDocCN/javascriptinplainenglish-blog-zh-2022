# JavaScript 中 DOM 节点的 tagName 和 nodeName 属性有什么区别？

> 原文：<https://javascript.plainenglish.io/whats-the-difference-between-the-tagname-and-nodename-property-of-a-dom-node-in-javascript-c9d15d64b2c7?source=collection_archive---------10----------------------->

![](img/b7753b96d9b30a745d26814c06dbe7d0.png)

Photo by [Khadeeja Yasser](https://unsplash.com/@k_yasser?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在一个 DOM 节点对象中，当我们检查一个 DOM 节点对象时，我们看到了`tagName`和`nodeName`属性。

在本文中，我们将看看 JavaScript 中 DOM 节点的`tagName`和`nodeName`属性之间的区别。

# JavaScript 中 DOM 节点的 tagName 和 nodeName 属性之间的区别

大多数情况下，DOM 节点的`tagName`和`nodeName`属性并不相同。

只有当节点是元素节点时才是一样的。

例如，如果我们有下面的 HTML:

```
<div class="a">a</div>
```

然后，我们可以通过编写以下内容来记录每种类型节点的`nodeName`和`tagName`的值:

```
const div = document.querySelector('div')
console.log(div.nodeType)
console.log(div.nodeName)
console.log(div.tagName)const attributeNode = div.getAttributeNode('class')
console.log(attributeNode.nodeType)
console.log(attributeNode.nodeName)
console.log(attributeNode.tagName)const childNode = div.childNodes[0]
console.log(childNode.nodeType)
console.log(childNode.nodeName)
console.log(childNode.tagName)
```

`div`是表示 div 的元素节点。

控制台日志记录以下值:

`div.nodeType`是 1。

`div.nodeName`和`div.tagName`都是`'DIV'`。

`attributeNode`是 div 的`class`属性的属性节点。

`attributeNode.nodeType`是 2。

`attributeNode.nodeName`为`'class'`，`div.tagName`为`undefined`。

`childNode`是 div 文本内容的 DOM 节点。

`childNode.nodeType`是 3。

因为`childNode`是文本节点而`div.tagName`是`undefined`，所以`childNode.nodeName`是`'#text'`。

所以我们可以看到`nodeName`和`tagName`只是元素相同。

# 结论

对于 DOM 元素，`nodeName`和`tagName`都被设置为元素的标签名作为它们的值。

但是，对于非元素节点，它们的值会有所不同。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****