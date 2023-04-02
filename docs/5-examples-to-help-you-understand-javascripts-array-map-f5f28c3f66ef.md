# 5 个例子帮助你理解 JavaScript 的数组。地图()

> 原文：<https://javascript.plainenglish.io/5-examples-to-help-you-understand-javascripts-array-map-f5f28c3f66ef?source=collection_archive---------8----------------------->

## [JavaScript](https://bookeraziz.medium.com/list/javascript-1ab814ee1c27)

## 关于数组你需要知道的一切。地图()。

![](img/52b2d90b86d11a31b83648e1cc401e7a.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

本文将教你如何使用 JavaScript 数组。Map()方法。数组。当您需要迭代一个数组并改变它的值时，Map()非常有用。

我将向您展示 **5 种不同的阵列示例。根据前一个例子提供的知识绘制(**)每个例子。

# 什么是数组。Map()？

在我们进入示例之前，理解数组的确切含义是很重要的。映射()是。

根据 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map):

> `map()`方法创建一个新的数组，其中填充了调用数组中每个元素的函数的结果。

本质上，map()方法所做的是运行我们提供的函数，并将其应用于数组中的每个元素。

关于 array.map()方法，有两件重要的事情需要了解:

1.  它不会**而不是**改变原始数组。它只将新值复制到一个新数组中
2.  数组**中项目的顺序**保持不变。

# 1.使用数组。Map()计算整数

数组最常见的用途。Map()正在对一个数字数组进行迭代，并执行某种形式的数学计算。

正如你在下面的例子中看到的，我们在数学计算中不仅仅局限于使用加法和减法。

Example of using Array.Map() to perform mathematical calculations

**元素**变量代表从原始数组处理的当前元素。

# 2.使用数组。Map()来改变字符串

我们不局限于改变整数值。我们也可以在字符串上使用 map()方法。

在下面的例子中，我们使用 map()方法通过使用 string.trim()方法来删除字符串数组中的空白。

Using Array.Map() to remove the whitespace from strings

# 3.从数组中获取当前索引。地图()

map()方法还允许您获取迭代的当前索引。

在下面的例子中，我们正在创建一个新的数组，它包含了原始数组中的元素及其当前索引。

Using the Array.Map() current index arguent

这个例子告诉我们两件事:

1.  我们可以通过 map()方法获得当前索引，方法是向回调函数提供一个**第二个值**(不必将其命名为 index，这只是标准约定)。
2.  我们可以从 map()方法返回**对象**。

# 4.使用数组。带有回调函数的 Map()

您可能不希望像我们之前使用的那样将 map()方法与内联函数一起使用。如果是这种情况，map()方法允许您使用回调函数。

在下面的例子中，我们使用 map()方法用一个城市名称的第一个和最后一个字符及其索引填充一个新数组。

如您所见，我们将它放在一个单独的 returnFirstAndLast 中，并将其传递给 map()方法。

这个例子告诉我们两个事情:

1.  如何在 map()方法中使用**回调函数**。
2.  只要顺序正确，你可以给变量取任何名字。*注意到我们如何在回调函数中使用 cityIndex 而不是 Index 了吗？*

# 5.用数组访问原始数组。地图()

您还可以从 map()方法中访问原始数组。

此示例将原始数组添加到新数组的每个元素中。

就我个人而言，我想不出有必要这样做的用例，但要完全理解 map()方法所提供的功能，知道这些仍然很重要。

# 结论

感谢您阅读完我关于**5 个示例的文章，这有助于您理解 JavaScript 的数组。【T7 地图()’。如果你有任何问题，请随意提问，我会尽快回答你。**

如果你刚接触媒体，你可以点击这里的链接[加入。](https://bookeraziz.medium.com/membership)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***