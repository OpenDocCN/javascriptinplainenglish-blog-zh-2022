# NodeList 和 HTML 集合有什么区别？

> 原文：<https://javascript.plainenglish.io/whats-the-difference-between-a-nodelist-and-an-html-collection-a0db0bd05de8?source=collection_archive---------7----------------------->

## 了解 NodeList 和 HTML 集合之间的区别，并找出哪一个最适合您的需要。

![](img/869fb0bf83ecd6c898408a42bf3fe79d.png)

Photo by [Surface](https://unsplash.com/es/@surface?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您是一名 web 开发人员，那么您可能以前听说过“节点列表”和“HTML 集合”这两个术语。但是它们是什么意思呢？它们之间有什么区别？在这篇博文中，我们将解释这两个术语之间的区别，并帮助您理解哪一个最适合您的需求。

## 什么是 HTML 集合？

HTML 集合是包含在 HTML 文档中的 HTML 元素的列表。这个列表可以通过索引来访问，它将返回该索引处的元素。HTML 集合是一个类似数组的结构，包含 HTML 元素。

## 什么是节点列表？

节点列表是包含在 HTML 文档中的节点列表。节点可以是从 HTML 元素到文本节点的任何东西。节点列表是一种类似数组的结构，包含节点。

## HTML 集合和节点列表之间的区别

HTML 集合和节点列表的主要区别在于，HTML 集合只包含 HTML 元素，而节点列表可以包含任何类型的节点。

另一个区别是 HTML 集合是动态的，这意味着如果底层文档发生变化，集合将会更新以反映这些变化。另一方面，节点列表并不总是动态的，如果底层文档发生变化，也不会总是更新。

HTML 集合不能访问数组方法，尽管它看起来像一个数组。NodeList 可以访问`forEach` 数组方法，这在您想要遍历节点时非常有用。

![](img/e4dba18132b830bf730211b5d794deb1.png)

Photo by [Nathan da Silva](https://unsplash.com/es/@silvawebdesigns?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 你应该用哪一个？

这个问题的答案取决于你的需求。如果您需要 HTML 元素的列表，那么 HTML 集合最适合您的需要。如果您需要一个节点列表，那么 NodeList 最适合您的需要。

通常，实时更新会导致难以修复的错误，所以如果有选择的话，NodeList 可能是最好的。

## 将 HTML 集合和节点列表转换为数组

但是，您可以将 HTML 集合和 NodeList 转换为数组，您可能会习惯于使用数组。这也允许您访问有用的数组方法，比如`map`、`forEach`、`filter`和`reduce`。

您可以使用`Array.from()`或 spread 操作符将 HTML 集合和 NodeList 转换成数组。

示例:

```
let newArr = Array.from(htmlCollection)let newArr = […htmlCollection]let newArr = Array.from(nodeList)let newArr = […nodeList]
```

我希望这篇文章教会你一些新的东西！祝你的编码项目好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*