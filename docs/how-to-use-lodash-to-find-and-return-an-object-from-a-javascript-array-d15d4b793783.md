# 如何使用 Lodash 从 JavaScript 数组中查找并返回一个对象？

> 原文：<https://javascript.plainenglish.io/how-to-use-lodash-to-find-and-return-an-object-from-a-javascript-array-d15d4b793783?source=collection_archive---------12----------------------->

![](img/20a6375cfdb147e9663f2939f42f203a.png)

Photo by [Hannes Egler](https://unsplash.com/@egla?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望使用 Lodash 从 JavaScript 数组中查找并返回一个对象。

在本文中，我们将了解如何使用 Lodash 从 JavaScript 数组中查找并返回一个对象。

# 使用查找方法

我们可以使用`find`方法找到一个带有谓词函数的对象，该函数返回我们正在寻找的对象的条件。

例如，我们可以写:

```
const arr = [{
    description: 'object1',
    id: 1
  },
  {
    description: 'object2',
    id: 2
  },
  {
    description: 'object3',
    id: 3
  },
  {
    description: 'object4',
    id: 4
  }
]const obj = _.find(arr, (o) => {
  return o.description === 'object3';
});
console.log(obj)
```

我们将数组作为第一个参数进行搜索。

我们传递谓词函数，它返回我们要寻找的对象的条件，作为第二个参数。

因此，`obj`是:

```
{description: "object3", id: 3}
```

我们还可以将一个对象作为第二个参数传入，以搜索具有给定值属性的对象:

```
const arr = [{
    description: 'object1',
    id: 1
  },
  {
    description: 'object2',
    id: 2
  },
  {
    description: 'object3',
    id: 3
  },
  {
    description: 'object4',
    id: 4
  }
]const obj = _.find(arr, {
  description: 'object3'
});
console.log(obj)
```

我们可以传入一个带有属性键和值的数组来执行相同的搜索:

```
const arr = [{
    description: 'object1',
    id: 1
  },
  {
    description: 'object2',
    id: 2
  },
  {
    description: 'object3',
    id: 3
  },
  {
    description: 'object4',
    id: 4
  }
]const obj = _.find(arr, ['description', 'object3']);
console.log(obj)
```

它们都得到了与第一个例子相同的结果。

# 结论

我们可以使用 Lodash `find`方法在一个数组中找到给定条件的对象。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*