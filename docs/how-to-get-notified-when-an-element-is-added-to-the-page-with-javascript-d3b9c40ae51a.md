# 如何在用 JavaScript 将元素添加到页面时得到通知？

> 原文：<https://javascript.plainenglish.io/how-to-get-notified-when-an-element-is-added-to-the-page-with-javascript-d3b9c40ae51a?source=collection_archive---------2----------------------->

![](img/c387b82ac524ad3b60660d4765dbf836.png)

Photo by [Önder Örtel](https://unsplash.com/@onderortel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在用 JavaScript 将元素添加到页面时得到通知。

在本文中，我们将研究如何在用 JavaScript 将元素添加到页面时得到通知。

# 使用变异观察器 API

观察 DOM 变化的最简单方法是使用大多数浏览器内置的 MutationObserver API。

要使用它，我们可以写:

```
const observerConfig = {
  attributes: true,
  childList: true,
  characterData: true
};const observer = new MutationObserver((mutations) => {
  mutations.forEach((mutation) => {
    console.log(mutation.type);
  });
});
observer.observe(document.body, observerConfig);setTimeout(() => {
  const div = document.createElement('div')
  document.body.appendChild(div)
}, 1500)
```

用`MutationObserver`构造函数观察 DOM 中的变化。

我们将带有`mutations`参数的回调传递给构造函数。

我们从那里得到应用于 DOM 的突变。

`mutation.type`已经完成了这种类型的变异。

我们应该将`'chilidsList'`和`'attributes'`视为值。

`'childList‘`是子节点的变化。

`'attributes'`是属性节点的变化。

我们用观察者的根元素调用`observer`，用`observerConfig`配置变异观察者如何观察变化。

`attributes`设置为`true`意味着我们观察属性节点的变化。

`childList`设置为`true`意味着我们监视子节点的变化。

# 结论

我们可以使用 MutationObserver API 来观察 JavaScript web 应用程序中 DOM 节点的变化。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****