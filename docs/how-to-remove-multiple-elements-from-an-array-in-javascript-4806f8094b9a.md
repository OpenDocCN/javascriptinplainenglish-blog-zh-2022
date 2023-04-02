# 如何在 JavaScript 中从数组中移除多个元素

> 原文：<https://javascript.plainenglish.io/how-to-remove-multiple-elements-from-an-array-in-javascript-4806f8094b9a?source=collection_archive---------1----------------------->

![](img/37de3a131cd2052329ebf6431104918b.png)

Photo by [Michael Dziedzic](https://unsplash.com/@lazycreekimages?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想从一个 JavaScript 数组中移除多个元素。

在本文中，我们将研究如何从 JavaScript 数组中移除多个元素。

# 使用 for-of 循环

从 JavaScript 数组中移除多个元素的一种方法是使用 for -of 循环。

例如，我们可以写:

```
const valuesArr = ["v1", "v2", "v3", "v4", "v5"],
  removeValFromIndex = [0, 2, 4];for (const i of removeValFromIndex.reverse()) {
  valuesArr.splice(i, 1);
}
console.log(valuesArr)
```

我们有`valuesArr`和我们想要移除的项目。

`removeValFromIndex`的索引包含我们想要删除的`valuesArr`的索引。

然后我们用`reverse`向后循环通过`removeValFromIndex`和 for-of 循环，用`splice`移除每个项目。

我们必须向后循环，这样我们就不会弄乱尚未删除的项目的索引。

所以，`valuesArr`就是`[“v2”, “v4”]`。

# 使用 Array.prototype.filter

此外，我们可以使用 JavaScript array `filter`方法从数组中移除项目，给定我们想要移除的项目的索引。

例如，我们可以写:

```
const valuesArr = ["v1", "v2", "v3", "v4", "v5"],
  removeValFromIndex = [0, 2, 4];const filtered = valuesArr.filter((value, index) => {
  return !removeValFromIndex.includes(index);
})
console.log(filtered)
```

我们用一个回调函数调用`filter`，这个回调函数将`index`参数作为第二个参数。

然后我们用`index`调用`includes`，看看`index`是否不在`removeValFromIndex`中。

如果不是，那么我们在返回的数组中保留给定索引的项。

所以，`filtered`就是`[“v2”, “v4”]`。

# 结论

从 JavaScript 数组中移除多个元素的一种方法是使用 for -of 循环。

此外，我们可以使用 JavaScript array `filter`方法从数组中移除项目，给定我们想要移除的项目的索引。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***