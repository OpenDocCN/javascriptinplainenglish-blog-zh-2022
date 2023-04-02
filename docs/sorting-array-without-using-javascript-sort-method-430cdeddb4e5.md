# 如何在不使用 JavaScript 的排序方法的情况下对数组排序

> 原文：<https://javascript.plainenglish.io/sorting-array-without-using-javascript-sort-method-430cdeddb4e5?source=collection_archive---------4----------------------->

![](img/ff1b88d425fd037d24551a2bef36a8e8.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在从事软件项目时，我们经常需要对数据进行分类。不出所料，在 JavaScript 中，数组有一个内置的方法`Array#sort`,用于对数组进行排序。

`Array#sort`方法采用一个回调函数，该函数应该返回一个用于对数组排序的整数。您可以在 [MDN docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 中详细了解分类方法。如果你想深入了解 V8 引擎中排序是如何实现的，你也可以在这里阅读。

在某些情况下，使用`Array#sort`会导致代码不可读。其中一种情况是排序项目不遵循任何时间顺序。例如，假设有一些数据要排序，数据的形状是:

```
interface Object {
    _id: string,
    status: 'Matched' | 'Active' | 'Paused' | 'Completed' | 'Cancelled'
}
```

数据应该按`status`排序，但排序的顺序是:`Matched > Active > Paused > Completed > Cancelled`，这意味着:带有`status == 'Matched'`的项目应该首先出现在列表中。有`status == 'Active'`的项目应该出现在其后，依此类推。

要对这种类型的数据进行排序，可以首先按属性对列表进行分组，然后使用预定义的标准列表将其映射到排序列表中。

```
import { groupBy } from 'lodash';const groupedData = groupBy(data, 'status');const ascOrder = [
    'Matched','Active','Paused','Completed','Cancelled'
];const sortedData = ascOrder
    .flatMap(status => groupedData[status])
    .filter(isNotEmpty)
```

这里使用了`flatMap`而不是`map`，因为`map`会给出一个嵌套数组，而该数组需要单独展平。此外，使用`Array#filter`是因为有可能某些状态没有项目，这会将`holes`留在结果数组中。

你可以在 [StackBlitz](https://stackblitz.com/edit/typescript-gspi36?embed=1&file=index.ts) 上看到完整的例子。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*