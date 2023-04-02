# JavaScript:解释 replaceAll()方法

> 原文：<https://javascript.plainenglish.io/javascript-explaining-the-replaceall-method-f4f3b79dcb3d?source=collection_archive---------13----------------------->

## `replaceAll()`方法如何工作，如何弥补`replace()`的不足。

![](img/6944b095f86b7e46ff7e409809fd13e6.png)

Photo by [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 最近引入了`replaceAll()`方法。这种新方法类似于`replace()`方法，但有一些关键区别。在本文中，我们将看看`replaceAll()`方法是如何工作的，以及它如何弥补`replace()`的缺点。

## 替换的动机()

引入`replaceAll()`方法是为了提供一种一致的方式来执行字符串替换。在此之前，JavaScript 开发人员使用的是`replace()`方法，它只是用来替换搜索字符串的第一个实例。这可能会导致代码不一致，尤其是当您试图替换一个搜索字符串的多个实例时。

`replaceAll()`方法提供了一种返回新字符串的方法，其中搜索字符串的所有匹配项都被指定的替换参数所替换。

## 句法

`replaceAll()`方法有两个参数。第一个参数是子字符串。第二个参数是将用于替换子字符串的所有匹配的字符串。第二个参数也可以是为每个匹配调用的函数。

我们可以通过下面的例子来观察`replaceAll()`方法的功能:

在上面的例子中，我们创建了一个字符串。然后，我们调用字符串上的`replaceAll()`方法，并传入“JavaScript”作为第一个参数，传入“Python”作为第二个参数。`replaceAll()`方法用“Python”替换了“JavaScript”的所有实例。

## 结论

`replaceAll()`方法提供了一种返回新字符串的方法，其中搜索字符串的所有匹配项都被指定的替换参数所替换。`replaceAll()`方法类似于 `replace()`方法，但是它不是只替换搜索字符串的第一个实例，而是替换所有实例。

希望这篇文章教会你一些东西！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****