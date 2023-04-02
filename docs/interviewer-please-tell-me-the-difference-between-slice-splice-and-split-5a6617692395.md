# 面试官:请告诉我切片、拼接和分割的区别？

> 原文：<https://javascript.plainenglish.io/interviewer-please-tell-me-the-difference-between-slice-splice-and-split-5a6617692395?source=collection_archive---------14----------------------->

## 你打算怎么回复他？

![](img/d23cf817390894c2a9ce371196d3fefe.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你在面试中被问到这个问题，你会如何回应面试官？Slice、Splice 和 Split 在拼写方面非常相似，很容易导致混淆。在本文中，我将为您详细解释它们各自的用法。虽然有点无聊，**耐心看完一定会有回报的。**我们开始吧！

# Array.prototype.slice()

**概述:**

`Array.prototype.slice(start, end)`方法返回子数组切片的**浅拷贝**，它是通过选择原始数组中从头到尾(不包括结尾)都带有下标的部分得到的。值得注意的是，原数组**不会被修改**。

**参数:**

`start`

*   这是一个可选参数，指示提取的起始索引。
*   如果没有定义，**默认为 0** 。
*   如果大于数组的索引范围，则返回空数组。
*   如果是负数，则表示从数组末尾的偏移量。当绝对值小于数组长度时，**等于** **这个负数加上数组长度**，如果绝对值大于等于数组长度，**等于 0** 。

`end`

*   可选参数，表示在索引前提取，即**不包括结束索引项**。
*   如果没有定义，**默认为数组**的长度。
*   如果大于数组索引范围，**默认为数组长度**。
*   如果是负数，则表示从数组末尾的偏移量。当绝对值小于数组长度时，**等于** **的负数加上数组长度**。如果绝对值大于或等于数组长度，**等于 0** 。

**返回值:**

提取的子数组片段的浅拷贝，可以在我之前的帖子中找到浅拷贝 vs 深拷贝的特性[。](https://levelup.gitconnected.com/use-pure-javascript-to-get-a-perfect-deep-copy-5fdc2d9e3d42)

**举例:**

# Array.prototype.splice()

**概述:**

`Array.prototype.splice(start, deleteCount, item1, item2, itemN)`方法可以在指定的索引处删除或添加一个元素，**它将改变原来的数组。**

**参数:**

`start`

*   必需的参数，指示开始改变数组的索引。
*   如果未定义，**什么都不会发生**。
*   如果大于数组的索引范围，**默认为** **数组的长度**。在这种情况下，无论 deleteCount 是什么，**元素** **都不会被删除**，只会根据`item1, item2, itemN`增加新的元素。
*   如果是负数，则表示从数组末尾的偏移量。当绝对值小于数组长度时，**等于** **的负数加上数组长度**。如果绝对值大于或等于数组长度，**则等于 0。**

`deleteCount`

*   可选参数，代表从起始索引开始要移除的元素**的数量。**
*   如果未定义，**默认情况下从数组开始到结束的所有元素都被删除。**
*   如果大于或等于从开始到结束的所有元素的个数，**从数组开始到结束的所有元素都被删除。**
*   如果为 0 或负值，**不删除任何元素。**

**项目 1、项目 2、项目 N:**

它们是可选参数，表示要从起始索引添加到数组中的元素。

**返回值:**

已移除元素的数组。如果没有移除任何元素，则返回一个空数组。

**例子:**

# String.prototype.split()

**概述:**

`String.prototype.split(separator, limit)`方法根据分隔符分割字符串，并将子字符串放入数组中。如果传入 limit 参数，它将返回长度为 limit 的结果数组。

**参数:**

`separator`

*   描述拆分模式的可选参数**，可以是字符串，也可以是正则表达式。**
*   如果未定义，返回的数组只包含**字符串的单个元素**。
*   如果 separator 是空字符串("")，str 将被转换为包含其每个 **UTF-16 "字符"**的字符串数组，注意这将中断[代理对](https://unicode.org/faq/utf_bom.%20html#utf16-2)。另请参见[堆栈溢出](https://stackoverflow.com/questions/4547609/how-to-get-character-array-from-a-string/34717402#34717402)。

`limit`

*   可选参数，指定分割后数组的最大长度**。**
*   如果为负或未定义，**不影响返回的拆分数组。**
*   如果为 0，**返回一个空数组。**

**返回值:**

*   当分隔符是字符串时，它从原始字符串中删除分隔符，并返回分隔的子字符串。
*   当分隔符是带有捕获括号的正则表达式时，每次分隔符匹配时，捕获括号的结果(包括任何未定义的结果)都被拼接到输出数组中。
*   如果分隔符的数据类型不是上述两项的类型，则默认强制转换为字符串类型，然后进行分隔。

**例子:**

# 总结

`Array.prototype.splice()`和`Array.prototype.slice()`是数组原型上的方法，它们的语法和特性不同，slice 不改变原始数组，splice 改变。

`String.prototype.slice()`是字符串原型上的一个方法，类似于数组原型上的 slice 方法，只是用字符串代替了。

`String.prototype.split()`是拆分一根弦，常与`Array.prototype.join()`连用。

最后，我是李。我会继续输出前端技术相关的故事。如果你喜欢这样的故事，想支持我，请考虑成为 [*中等会员*](https://medium.com/@islizeqiang/membership) *。每月 5 美元，你可以无限制地访问媒体内容。如果你通过* [*我的链接*](https://medium.com/@islizeqiang/membership) *报名，我会得到一点佣金。*

你的支持对我来说很重要——谢谢。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*