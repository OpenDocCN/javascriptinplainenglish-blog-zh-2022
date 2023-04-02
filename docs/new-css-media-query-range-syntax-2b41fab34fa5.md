# 新的 CSS 媒体查询范围语法

> 原文：<https://javascript.plainenglish.io/new-css-media-query-range-syntax-2b41fab34fa5?source=collection_archive---------11----------------------->

## 这个月早些时候，新语法登陆了 Chrome！

![](img/d1235e096f9c8a9cdf2d1369de5af74f.png)

Photo by [Samuel Regan-Asante](https://unsplash.com/@fkaregan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

媒体查询的新范围语法是我最期待的关于响应式设计的 CSS 特性之一。我一直不喜欢在媒体查询中写最大宽度和最小宽度。对我的心态或我的代码来说，这不太自然。最后，这里有一个在最新的 Chrome 和 Firefox 浏览器中工作的新方法(不幸的是，我没有听到任何关于 Safari 的消息，如果你知道他们的进展，请在评论中与来源分享)。

## 用 CSS 编写媒体查询的新方法

媒体查询级别 4 处于 CSS 规范的 CR 状态。因此，它的一些功能可能会发生变化。然而，我们仍然可以研究规范的范围语法，因为它应该保持原样。我们还可以预期，我们将能够对容器查询使用相同的语法。

```
@media (width > 400px) {
  ...
}
```

我们终于可以使用有意义并反映常见编程比较的运算符了！

```
@media (width >= 400px) {
  ...
}
```

此外，这将工作(400 像素和 1000 像素之间的视口):

```
@media (400px <= width <= 1000px) {
  ...
}
```

直到最近，我们还不得不这样写上面的例子:

```
@media (min-width: 400px) and (max-width: 1000px) {
  ...
}
```

现在简单多了！范围查询也适用于否定:

```
@media not (width > 400px) {
  ...
}
```

请注意，范围查询语法是最小值/最大值的一种简写。因此，**下面的**是无效的:

```
/* won't work */
@media (min-width > 400px) {
  ...
}
```

## 坏消息是:浏览器支持

由于这是几天前在 Chrome 上登陆的一个功能，一般的支持是很糟糕的(尽管 Firefox 在早期确实支持这个功能)。【https://caniuse.com/css-media-range-syntax】看这里:[T4](https://caniuse.com/css-media-range-syntax)

然而，这是一个令人兴奋的新功能，一旦它得到所有浏览器供应商的更好支持，它将使我们的生活变得更容易。

你最期待但仍缺乏支持的 CSS 新特性是什么？

就这些了，伙计们！

如果你想阅读更多这样的文章，请留下关注、鼓掌或评论。只有得到你的反馈，我才知道你想读什么。

非常感谢您的阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***