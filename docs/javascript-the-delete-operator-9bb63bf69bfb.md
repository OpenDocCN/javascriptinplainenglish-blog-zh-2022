# JavaScript:删除操作符

> 原文：<https://javascript.plainenglish.io/javascript-the-delete-operator-9bb63bf69bfb?source=collection_archive---------14----------------------->

![](img/8e57f152228e322f9585b06b6163b458.png)

Photo by [Thought Catalog](https://unsplash.com/@thoughtcatalog?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`delete` 运算符是 JavaScript 中最重要的运算符之一。这是一个强大的工具，可用于从数组和对象中移除项目。在本文中，我们将讨论`delete` 操作符是如何工作的，并提供一些如何使用它的例子。

## 什么是删除操作符？

`delete` 操作符是一个一元操作符，它接受一个操作数，如果操作成功，则返回 true。`delete`操作符接受两个参数。第一个参数是我们希望删除其属性的对象。第一个参数可以是普通的旧 JavaScript 对象(POJO)或数组。第二个参数是要删除的属性的名称。

如果在一个对象上使用了`delete` 操作符，它将从该对象中删除指定的属性。如果在数组上使用了`delete` 操作符，它将从数组中删除指定的元素。需要注意的是，使用`delete` 操作符删除一个属性将导致该属性不再可访问。

## 从对象中删除属性

我们可以使用`delete` 操作符从对象中删除一个属性。当我们从对象中删除一个属性时，该属性将从对象中移除，并且不能再被访问。以下示例显示了如何从对象中删除属性:

![](img/9458b8802cea8778152f213853145dfe.png)

Photo by [Aleksander Vlad](https://unsplash.com/@aleksowlade?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 从数组中删除元素

我们也可以使用`delete` 操作符根据索引从数组中删除一个元素。当我们从数组中删除一个元素时，这个元素就从数组中移除了，并且不能再被访问。以下示例显示了如何从数组中删除元素:

正如我们所看到的，当我们从数组中删除一个元素时，被删除的元素被替换为一个空值。这是因为删除数组元素不会影响数组的长度。

需要注意的是`delete` 操作符不影响数组中元素的顺序。从数组中删除一个元素不会改变数组中其他元素的索引。

## 结论

总之，`delete`操作符是一个强大的工具，可以用来从数组和对象中移除项目。当您需要重构从数组或对象返回的内容时,`delete` 操作符会很有帮助。

我希望这篇文章能消除你的任何困惑！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*