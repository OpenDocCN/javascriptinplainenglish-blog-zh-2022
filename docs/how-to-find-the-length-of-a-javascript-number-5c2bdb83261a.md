# 如何求一个 JavaScript 数的长度？

> 原文：<https://javascript.plainenglish.io/how-to-find-the-length-of-a-javascript-number-5c2bdb83261a?source=collection_archive---------0----------------------->

![](img/afdac46ffca7eba0e9e6906b7b1d55a7.png)

Photo by [Şahin Sezer Dinçer](https://unsplash.com/@sahinsezerdincer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们希望在我们的 JavaScript 应用程序中找到一个 JavaScript 数字的长度。

在本文中，我们将看看如何找到一个 JavaScript 数字的长度。

# 将数字转换为字符串，并使用字符串的 length 属性

查找 JavaSdcript 数字长度的一种方法是将数字转换成字符串，然后使用字符串的`length`属性来获取数字的长度。

例如，我们可以写:

```
const x = 1234567;
console.log(x.toString().length);
```

我们有号码`x`。

然后我们在它上面调用`toString`，把它转换成一个字符串。

然后我们使用`length`属性返回它的长度。

因此，控制台日志应该记录 7。

# 使用 Math.ceil 和 Math.log 方法

我们可以得到以 10 为底的数的对数，从而得到一个数的长度。

为此，我们可以使用`Math.log`来获得数字的自然对数。

然后我们可以将返回的结果除以`Math.LN10`转换成同个数的底数为 10 的对数。

然后我们调用其中的`Math.ceil`,将其向上舍入到最接近的整数，以获得长度。

例如，我们可以写:

```
const x = 1234567;
const len = Math.ceil(Math.log(x + 1) / Math.LN10);
console.log(len);
```

去做这一切。

我们给`x`加 1，以避免在`x`为 0 时取 0 的对数。

然后我们得到`len`是 7。

# 使用 Math.ceil 和 Math.log10 方法

ES6 附带了`Math.log10`方法来获取以 10 为基数的对数。

为了使用它，我们写:

```
const x = 1234567;
const len = Math.ceil(Math.log10(x + 1));
console.log(len);
```

我们用`x + 1`调用`Math.log10`以避免在`x`为 0 时取 0 的对数。

我们再次使用`Math.ceil`将对数向上舍入到最接近的整数。

所以我们应该得到和其他例子一样的结果。

# 结论

我们可以用各种 JavaScript 数学方法找到一个数字的长度，或者将它转换成一个字符串并使用`length`属性。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*