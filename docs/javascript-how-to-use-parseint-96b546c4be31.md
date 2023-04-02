# JavaScript:如何使用 parseInt()

> 原文：<https://javascript.plainenglish.io/javascript-how-to-use-parseint-96b546c4be31?source=collection_archive---------8----------------------->

## 仔细看看如何在 JavaScript 中使用 parseInt()函数将字符串转换为整数。

![](img/c8caeb76859c2ca26c7af590c213d2b9.png)

Photo by [Alexandra Fuller](https://unsplash.com/@alexandrajf?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

谈到 JavaScript，有许多内置函数可以让您的生活变得更加轻松。在本文中，我们将研究其中的一个特性:`parseInt()`。此函数允许您将字符串转换为整数，这在处理数据时非常有用。让我们仔细看看这个函数是如何工作的！

## 句法

parseInt 的语法非常简单:

```
parseInt(string, radix);
```

字符串是要转换为整数的值。radix 是一个可选参数，用于指定数字的基数。如果不指定基数，函数将根据字符串推断使用什么基数。

如果没有提供 radix 参数，并且字符串以 0x 开头，则该函数将假定您正在尝试转换一个十六进制数，并将半径默认为 16。否则，该函数将假定您正在处理一个十进制数，并将基数默认为 10。

## parseInt()如何工作

现在我们知道了语法，让我们看看`parseInt()`在实践中是如何工作的。在下面的示例中，我们有一个包含数字的字符串:

```
let numString = “42”;
```

我们可以用`parseInt()`将这个字符串转换成一个整数:

```
let num = parseInt(numString);console.log(num); // 42
```

如您所见，`parseInt()`函数成功地将我们的字符串转换成了整数。需要记住的一点是，如果你试图转换的字符串不是一个有效的数字，`parseInt()`将返回`NaN`:

```
let invalidString = “This is not a number”;let num = parseInt(invalidString);console.log(num); // NaN
```

这两个例子非常简单，但是`parseInt()`可能会有一些令人困惑的行为。让我们来看几个可能会让你犯错的例子。

![](img/4ceec43ac2507b881c2277b76caeb668.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 漂浮物

`parseInt()`忽略浮点值。可以利用这个功能，因为`parseInt()`可以用来将浮点数转换成整数。在下面的例子中，我们有一个值为 42.23 的浮点数:

```
let floatNum = 42.23;console.log(parseInt(floatNum)); // 42
```

如您所见，`parseInt()’s`功能导致输入忽略浮点值，只将整数 42 转换成整数。

## 在字符串中混合数字

如果您有一个既包含数字又包含非数字的字符串，`parseInt()`将只返回第一个非数字字符之前的数字的整数值:

```
let mixedString = “42 This is a string!”;console.log(parseInt(mixedString)); // 42
```

如您所见，只返回了整数值“42 ”,字符串的其余部分被忽略。但是，如果字符串以非数字字符开头，那么`parseInt()`将返回`NaN`:

```
let mixedString = “This is a string123!”;console.log(parseInt(mixedString)); // NaN
```

## 结论

在本文中，我们学习了 JavaScript 中的`parseInt()`函数。这个函数允许我们将字符串转换成整数，这在处理数据时非常有用。我们还了解了该函数的工作原理，以及在使用它时可能会遇到的一些问题。

我希望这篇文章能消除你对`parseInt()`的任何疑惑！祝你的编码面试好运！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****