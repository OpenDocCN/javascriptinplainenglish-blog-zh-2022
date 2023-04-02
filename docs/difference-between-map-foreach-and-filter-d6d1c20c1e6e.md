# JavaScript 中 map()、forEach()和 filter()的区别

> 原文：<https://javascript.plainenglish.io/difference-between-map-foreach-and-filter-d6d1c20c1e6e?source=collection_archive---------3----------------------->

## JavaScript 中的 map()、forEach()和 filter()方法有何不同

![](img/c3c4253cf82fa976a533868f3c57b76f.png)

Photo by [Tine Ivanič](https://unsplash.com/@tine999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是世界上最流行的编程语言，被广泛用于 web 开发。具有 JavaScript 背景的开发人员可以很容易地接触到 React 等前端库。

这使得 JavaScript 成为专业人士的必备语言。由于 JavaScript 的广泛使用，它为新生/专业人士提供了很多就业机会。如果您正在准备 JavaScript 面试，map()、forEach()和 filter()方法之间的区别是最常见的问题。

# **地图()**

`map()`函数接收一个函数作为参数，并将代码应用于每个元素并返回一个全新的数组。它不会改变原始数组。
map()函数返回一个新的数组，因此只有当你打算使用返回的数组时才应该使用它，否则你应该更喜欢 forEach()函数。

语法:

```
map((element) => { /* Coding Logic*/ })
map((element, index) => { /* Coding Logic */ })
map((element, index, mapArray) => { /* Coding Logic */ })
```

注意:这里的`mapArray`是调用 map()函数的数组。

示例:

Map Function Example

如示例所示，我们应用了一个函数，该函数期望每个数组元素都乘以 2。map()方法不改变原始数组。它将返回一个新的数组。我们可以使用返回的数组进行进一步的操作。

# **forEach()**

`forEach()`函数接收一个函数作为参数，并对每个元素应用相同的代码。它不会返回任何内容，只是将条件应用于每个元素。它不会改变原始数组。

`forEach()`方法的返回值为**未定义**。`forEach()`方法不会等到承诺兑现。

语法:

```
forEach((element) => { /* Coding Logic */ })
forEach((element, index) => { /* Coding Logic */ })
forEach((element, index, array) => { /* Coding Logic */ })
```

由于`forEach()`返回 undefined，我们不能附加任何 JavaScript 方法，比如 Filter 或 reduce。只有当我们不打算对迭代值应用任何进一步的操作时，才应该使用它。

ForEach Function Example

# **过滤器()**

`filter()`方法接收函数作为参数。它对数组中的每个元素运行函数。它将返回满足应用条件的新数组。它不会改变原始数组。

语法:
`filter((element) => { /* … */ } )
filter((element, index) => { /* … */ } )
filter((element, index, array) => { /* … */ } )`

如果没有值与元素匹配，filter()方法将返回一个空数组**。如果发生任何匹配，它将返回一个匹配值的**数组**。由于它可能返回一个新的数组，我们可以使用其他方法，如 reduce，splice with filter()方法。**

Filter Function Example

如示例所示，filter()方法将返回一个新数组，其中包含与回调函数匹配的元素。

我们已经分别详细了解了 map()、forEach()和 filter()方法的语法、工作和返回值，这里我们将总结所有要点。

# **差异**

*   **返回值**
    `map()` 将根据应用的条件返回一个**新数组**。
    `forEach()`不会返回任何东西。`forEach()`返回**未定义的**。方法将返回一个匹配元素的数组，否则如果没有匹配将返回一个空数组。
*   如果你需要修改当前的数组，并且期待一个修改过的数组，那么你应该选择`map()`。
    如果只是想迭代数组，那么可以用`forEach()`。
    如果你期望从给定的数组中得到过滤后的值，那么你应该使用`filter()`方法。
*   由于 `forEach()`返回 undefined，所以不能附加其他类似`filter()`的函数。
    用`map()`可以轻松套用`filter()`。
    其他 JavaScript 方法可以附加在`filter()`方法上。

本文到此为止。如果你觉得这篇文章有帮助，那么请检查其他文章。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***