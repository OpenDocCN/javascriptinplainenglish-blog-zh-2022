# 如何在 JavaScript 中检查一个值是否在一个数字范围内

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-value-is-within-a-range-of-numbers-in-javascript-6d989ae2e6a1?source=collection_archive---------0----------------------->

![](img/d4c92c08f88effad7c21eb39136921d6.png)

Photo by [Pawel Kadysz](https://unsplash.com/@pawelkadysz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想要检查一个值是否在 JavaScript 中的一个数字范围内。

在本文中，我们将看看如何在 JavaScript 中检查一个值是否在一个数字范围内。

# 使用大于或等于和小于或等于运算符

我们可以使用 JavaScript 的大于或等于和小于或等于操作符来检查一个数字是否在两个数字之间。

例如，我们可以写:

```
const between = (x, min, max) => {
  return x >= min && x <= max;
}
// ...
const x = 0.002
if (between(x, 0.001, 0.009)) {
  // something
}
```

我们用`x`、`min`和`max`参数创建了`between`函数。

`x`是我们要检查它是否在`min`和`max`之间的数字。

然后我们在`if`语句中调用它，看看`x`是否在 0.001 到 0.009 之间。

# 使用 Lodash inRange 方法

我们还可以使用 Lodash `inRange`方法来检查一个数字是否在两个数字之间。

为了使用它，我们写:

```
const x = 0.002
if (_.inRange(x, 0.001, 0.009)) {
  // something
}
```

我们用数字`x`调用`inRange`来检查它是否在 0.001 和 0.009 之间。

# 结论

我们可以使用 JavaScript 的大于或等于和小于或等于操作符来检查一个数字是否在两个数字之间。

同样，我们可以使用 Lodash `inRange`方法来做同样的事情。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****