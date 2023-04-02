# 如何用 JavaScript 获取一个数的位数

> 原文：<https://javascript.plainenglish.io/how-to-get-the-number-of-digits-of-a-number-with-javascript-7fd88e5e5381?source=collection_archive---------6----------------------->

## 用 JavaScript 获取数字位数的教程。

![](img/b0ac3430baaad2d98638f54b27f550ee.png)

Photo by [Elisa](https://unsplash.com/@mercoledi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 得到一个数的位数。

在本文中，我们将看看如何用 JavaScript 获得一个数字的位数。

# 使用 Number.prototype.toString 方法

我们可以用`Number.prototype.toString`方法得到一个非负整数的位数。

例如，我们可以写:

```
const getLength = (number) => {
  return number.toString().length;
}
console.log(getLength(12345))
```

得到 12345 的位数。

为此，我们创建了接受`number`参数的`getLength`函数。

我们返回`number`的字符串形式的`length`。

因此，控制台日志应该记录 5，因为 12345 有 5 个数字。

# 获取十进制数的位数

我们不能使用`toString`来获得十进制数字的位数，因为它只是返回数字的字符串形式，包括所有十进制数字和数字附带的其他字符。

为了得到十进制数的位数，我们可以使用数学方法。

例如，我们可以写:

```
const getLength = (number) => {
  return Math.max(Math.floor(Math.log10(Math.abs(number))), 0) + 1;
}
console.log(getLength(12345.67))
```

取 10 的对数加 1 得到`number`的位数。

我们必须确保用`Math.abs`将`number`转换成正数，这样我们就可以得到它的对数。

接下来，我们调用`Math.floor`来取对数的底值，以获得除最左边数字之外的位数。

然后我们用`Math.max`得到对数的底数和 0，加 1 得到位数。

因此，控制台日志应该记录 5，因为我们使用 log 操作来丢弃十进制数字。

# 结论

我们可以使用数学方法或者将一个数字转换成一个字符串来获得一个 JavaScript 数字的位数。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***