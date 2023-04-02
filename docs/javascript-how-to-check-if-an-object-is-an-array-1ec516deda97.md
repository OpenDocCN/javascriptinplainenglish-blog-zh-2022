# JavaScript:如何检查一个对象是否是数组

> 原文：<https://javascript.plainenglish.io/javascript-how-to-check-if-an-object-is-an-array-1ec516deda97?source=collection_archive---------8----------------------->

![](img/4da23315e6fd622c855ca2d80940159f.png)

Photo by [John Schnobrich](https://unsplash.com/@johnschno?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，有几种不同的方法来检查一个对象是否是一个数组。在本文中，我们将讨论三种最常见的方法:`Array.isArray()`、`instanceof` 操作符，以及利用`Object.prototype`中的`toString`方法。我们还将提供如何使用每种方法的例子。

## Array.isArray()

`Array.isArray()`方法是一种现代方法，用于确定一个对象是否是一个数组。此方法返回一个布尔值:如果对象是数组，则为 true 如果对象不是数组，则为 false。这个方法是检查一个对象是否是一个数组的最直观和直接的方法。

要使用`Array.isArray()`方法，我们只需传入想要检查的对象:

```
Array.isArray([]) // true
Array.isArray({}) // false
```

从上面的例子中我们可以看出，如果对象是数组，`Array.isArray()`返回 true，如果对象不是数组，则返回 false。

## 运算符的实例

另一种检查对象是否为数组的方法是使用`instanceof` 操作符。如果对象是指定构造函数的实例，则`instanceof` 运算符返回 true。在这种情况下，我们希望检查对象是否是数组构造函数的实例。

下面是我们如何使用`instanceof` 操作符检查一个对象是否是一个数组:

```
[] instanceof Array // true
{} instanceof Array // false
```

正如我们所见，`instanceof` 操作符的行为类似于`Array.isArray()`方法。如果对象是数组，则返回 true，如果对象不是数组，则返回 false。

![](img/26480a01f28ea7acd1b73c1d45345093.png)

Photo by [Adolfo Félix](https://unsplash.com/@adolfofelix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 利用 toString 方法

检查对象是否为数组的另一种方法是利用来自`Object.prototype`的`toString` 方法。`toString`方法是一个内置方法，它返回一个对象的类的字符串表示。当在数组上调用这个方法时，它返回字符串`“[object Array]”`。

我们可以通过下面的代码使用这个方法来检查一个对象是否是一个数组:

```
Object.prototype.toString.call([]) // "[object Array]"
Object.prototype.toString.call({}) // "[object Object]"
```

正如我们看到的，这个方法在数组上调用时返回字符串`“[object Array]”`，在对象上调用时返回`“[object Object]”`。该方法可用于检查对象是否为数组，但不如`Array.isArray()`方法或`instanceof` 操作符直观。

## 结论

总之，在 JavaScript 中有几种不同的方法来检查一个对象是否是一个数组。最常见的方法是`Array.isArray()`、`instanceof` 运算符，以及利用`Object.prototype`中的`toString`方法。

希望这篇文章教会你一些东西！祝你的编码面试好运！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*