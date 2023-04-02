# 如何用条件元素定义 JavaScript 数组

> 原文：<https://javascript.plainenglish.io/how-to-define-a-javascript-array-with-conditional-elements-cffd2d1ecef7?source=collection_archive---------1----------------------->

## 一个关于定义一个 JavaScript 数组的教程，该数组中有条件地添加了元素。

![](img/86176b74a1be378899114ed6db74bc32.png)

Photo by [dylan nolte](https://unsplash.com/@dylan_nolte?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望有条件地将数组元素添加到 JavaScript 数组中。

在本文中，我们将研究如何定义一个 JavaScript 数组，其中有条件地添加元素。

# 使用扩展运算符

我们可以使用 spread 运算符有条件地将数组扩展到另一个数组中。

例如，我们可以写:

```
const items = [
  'foo',
  ...true ? ['bar'] : [],
  ...false ? ['falsy'] : [],
]console.log(items)
```

那么`items`就是`[“foo”, “bar”]`,因为我们有一个三元表达式，它的条件部分的值是`false`。

如果是`true`，那么左阵展开成`items`。

否则，空数组被展开到`items`。

# 有条件地调用 Array.prototype.push

另一种有条件地向 JavaScript 数组添加条目的方法是使用`push`方法。

例如，我们可以写:

```
const items = [
  'foo',
]if (true) {
  items.push("bar");
}if (false) {
  items.push("false");
}console.log(items)
```

然后`'bar'`被附加到`items`上，但`'false'`没有。

这是因为第一个 conditionally 将`true`作为条件，第二个 conditionally 将`false`作为条件。

因此`items`又是`[“foo”, “bar”]`。

# 结论

我们可以使用 spread 操作符有条件地将项目分散到一个数组中。

我们还可以有条件地调用`push`来有条件地将项目添加到 JavaScript 数组中。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。**