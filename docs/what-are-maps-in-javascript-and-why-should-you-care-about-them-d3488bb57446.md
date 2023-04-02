# JavaScript 中的地图是什么，为什么要关心它们？

> 原文：<https://javascript.plainenglish.io/what-are-maps-in-javascript-and-why-should-you-care-about-them-d3488bb57446?source=collection_archive---------16----------------------->

## 关于 JavaScript 中的地图，你需要知道的一切。

![](img/36927bb7808d50659ac561b4884897cc.png)

Photo by [Bailey Burton](https://unsplash.com/@17thcw?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在 JavaScript 中有不同的方法来存储变量。最常见的方法是数组、集合和映射。准确地说，集合只存储唯一类型的数据。这有时会导致一些问题，因为从用户的角度来看，重复数据可能是有价值的。

另一方面，数组并不局限于唯一类型的数据，相同类型的数据可以在一个数组中重复，这为用户和开发人员提供了灵活性。

可能有这样一种情况，开发人员需要能够保存“键-值”对类型数据的东西。在这种情况下，最佳方式是使用地图。尽管在 JavaScript 中有各种方法来存储“键-值”对，但是 map 确保您可以使用任何类型的数据作为键。

## 创建地图

创建地图就像创建数组一样简单。首先，让我们看看如何在 JavaScript 中创建数组，看看两者的相似之处。要创建一个数组，我们需要使用`const`关键字并在方括号内添加元素。让我们看一个例子——

```
Creating an array in JavaScriptconst fruits = ["apple", "orange", "grape"]Using const keyword is a good practise.
```

现在让我们来看看如何创建地图。为此，我们使用两种方法—

*   `new Map()`用于创建地图
*   `Map.set()` 给地图添加元素

```
Creating a Map in JavaScript We can create a Map by passing an array to it. const exampleMap = new Map ([["apples", 100],["orange",200],["grape",300]])You can add elements using Map.set()exampleMap.set("jackfruit",400)
```

## 处理元素

正如我们已经讨论过的，Map 存储了一个“键-值”对，因此我们可以通过使用返回那个键的值的`map.get(key)` 来调用它。如果在我们的地图上找不到钥匙，可能会简单地返回`undefined`。

让我们看看它的例子——

```
exampleMap.get("apples")
Returns 100exampleMap.get("orange")
Returns 200exampleMap.get("grape")
Returns 300
```

除此之外，您还可以使用`has()`方法来查看地图上是否有一个键。它不会返回键的值，但如果键出现在地图上，它将返回 true。

要查看地图的大小或检查地图中存在的元素数量，您可以简单地使用`size` it，它将返回地图的当前元素数量。你可以简单地把它当作—

```
exampleMap.size 
```

## 删除并清除

高效的内存管理对于优化代码是非常必要的。创建地图后，为了节省内存，你必须能够完全删除它。有时，您可能根本不需要该映射，或者只想删除与特定键相关联的单个值。

为此，您可以使用以下两种方法—

*   `map.delete(key)`它将简单地删除给定键的值。
*   这将从您的地图中移除所有内容

让我们用伪代码来看看—

```
To delete a value of orange we will use the delete methodexampleMap.delete("oranges")To remove everything from your map you will simply use clear methd exampleMap.clear()
```

map 是在 JavaScript 中存储“键-值”对的最佳方式，但是仍然有许多人不使用它，仅仅是因为缺乏关于它的信息。许多人试图利用一个可以像 Map 一样工作的数组，但是它没有 Map 那么高效。我希望这能让你对地图有一个微妙的了解，当你用 JavaScript 编程时，你会在任何需要的时候使用它。祝你的编程之旅好运！

[***用我的推荐链接给自己买一个 5 美元的中级会员，点击这里(我得到一小笔佣金，它直接支持我，不需要你额外付费)***](https://aniketz.medium.com/membership)

[](https://aniketz.medium.com/membership) [## 通过我的推荐链接加入 Medium-Aniket

### 阅读 Aniket 上的每一个故事(以及媒体上成千上万的其他作者)。你的会员费直接支持了一个市场…

aniketz.medium.com](https://aniketz.medium.com/membership) 

[***想加入我的时事通讯了解更多此类内容，请点击这里…***](https://aniketz.medium.com/subscribe)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***