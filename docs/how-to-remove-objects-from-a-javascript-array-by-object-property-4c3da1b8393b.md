# 如何通过对象属性从 JavaScript 数组中移除对象

> 原文：<https://javascript.plainenglish.io/how-to-remove-objects-from-a-javascript-array-by-object-property-4c3da1b8393b?source=collection_archive---------4----------------------->

## 关于如何从一个给定属性值的 JavaScript 数组中移除对象的教程。

![](img/7184838d8fbe546ad15cb9bc943f8442.png)

Photo by [hue12 photography](https://unsplash.com/@hue12_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望从 JavaScript 数组中移除一个具有给定属性值的对象。

在本文中，我们将研究如何在给定属性值的情况下从 JavaScript 数组中移除对象。

# 使用 Array.prototype.splice 和 Array.prototype.findIndex 方法

我们可以使用 JavaScript array `findIndex`方法在一个具有给定属性值的数组中查找对象的索引。

然后我们可以使用 JavaScript array `splice`方法移除带有由`findIndex`返回的索引的项目。

例如，我们可以写:

```
const items = [{
    id: 'abc',
    name: 'oh'
  },
  {
    id: 'efg',
    name: 'em'
  },
  {
    id: 'hij',
    name: 'ge'
  }
];
const index = items.findIndex((i) => {
  return i.id === "abc";
})
items.splice(index, 1);
console.log(items)
```

我们有一个包含一堆对象的`items`数组。

我们想去掉`id`设置为`'abc'`的那个。

为此，我们用一个返回`id.id === 'abc'`的回调函数调用`items.findIndex`，这样我们就可以在`id`设置为`'abc'`的情况下获取对象的索引。

然后我们可以用`index`和 1 调用`items.splice`来从`items`中移除给定`index`处的项目。

因此，`items`现在是:

```
[
  {
    "id": "efg",
    "name": "em"
  },
  {
    "id": "hij",
    "name": "ge"
  }
]
```

# 结论

我们可以使用`findIndex`方法来查找数组中满足给定条件的对象的索引。

然后，我们可以使用`splice`方法来移除由`findIndex`返回的索引处的项目，以从数组中移除该项目。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***