# 用 CSS 找到父元素

> 原文：<https://javascript.plainenglish.io/find-the-parent-node-via-css-e3b4baed1d94?source=collection_archive---------5----------------------->

## CSS ': `has'`添加了一个定制逻辑来基于其他选择器(而不是它自己的选择器)查找元素。

![](img/265171c2e775d27289fbee53c8235c44.png)

Photo by [Vinicius "amnx" Amano](https://unsplash.com/@viniciusamano?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我必须承认最强大的机器之一是 *CSS* 引擎，但有时仅使用 CSS 很难完成某些事情，甚至只是改变一些颜色。例如，如果我让你在 CSS 中从一个子元素中找到一个父元素，通常你会被卡住。

CSS 的设计方式是，给定一个元素，你可以指定它的子元素的可视属性。所以它或多或少是按照自顶向下的方法设计的，就像 HTML DOM 树一样。首先从作为根的元素开始，然后通过选择器深入到它的分支和叶子。

## Java Script 语言

我是一名 JavaScript 开发人员，所以在过去，当这些问题出现时，我只需编写几行 JS 代码，例如:

```
Document.getElementById('root')
```

有时是更复杂的版本，但或多或少我能找到元素，即使它在很远的 DOM 分支中。这里没有什么新的东西，我们在近二十年前就已经这样做了。但坦白说，JavaScript 很重；如果不是必须要做，我尽量不要用 JavaScript 来做。没错，我是一名 JavaScript 开发人员，但是最近我把 CSS 作为我解决 UI 问题的第一个工具，仅仅是因为它更便宜。

## 半铸钢ˌ钢性铸铁(Cast Semi-Steel)

信不信由你，CSS 每天都在增加新的功能。我们之所以觉得它变化很快，是因为没有人跟踪 CSS 规范，更不用说所有的浏览器兼容性了。似乎为我们打开了与父节点相关的大门的特性之一叫做`:has`。还不知道的可以看看视频。我会一直等到你回来。

我们不是直接找到一个元素，而是通过询问它是否有或包含另一个选择器来找到它。让我们回顾一下选择器:

```
a img {} 
```

上面的选择器要求`a`里面的`img`。这很简单，但这也是我们找不到家长的原因，因为我们对`img`不感兴趣，我们真正想做的是:

```
a:has(img) {}
```

啊，如果`a`包含一个`img`，那么那就是我们要找的`a`。就这样？你可能会说。是的，这真的是把不可能变成了可能。

> 检查`:has`、[https://developer.mozilla.org/en-US/docs/Web/CSS/:has](https://developer.mozilla.org/en-US/docs/Web/CSS/:has)的规格

## 正文:有()

所以很多时候我在做网站的时候，当一个模态弹出来的时候，我就想改变`body`的样式。现在在我看来，我只需要做到以下几点:

```
body:has(.Modal) {}   // if modal is inside
body:has(+ .Modal) {} // if modal is sibling
```

一行代码？让我们试着用 JavaScript 做上面的事情，祝你好运。此外，如果您可以在前端框架中集成少于五行代码的 JavaScript 版本。你赢了！

所以现在的问题不再是找到父节点，而是找到拥有某些东西的节点。在某种程度上，这为需要寻找远处元素的问题提供了另一种途径。**最重要的是，我们可以马上对找到的元素进行操作。**

# 摘要

CSS `:has`添加了一个定制逻辑来基于其他选择器(而不是它自己的选择器)查找元素。这将使寻找父节点的不可能任务从现在开始成为可能。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*