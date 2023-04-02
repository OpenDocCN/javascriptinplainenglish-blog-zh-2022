# 如何给 JavaScript 对象追加一个属性？

> 原文：<https://javascript.plainenglish.io/how-to-append-a-property-to-a-javascript-object-cd57e2ace1c7?source=collection_archive---------1----------------------->

![](img/ad52f7347f41b7bf5455f08ea4fa1b39.png)

Photo by [Joyful](https://unsplash.com/@joyfulcaptures?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们经常想在代码中给 JavaScript 对象添加新的属性。

在本文中，我们将了解如何向 JavaScript 对象追加属性。

# 使用 Object.assign 方法

将属性附加到 JavaScript 对象的一种方法是使用`Object.assign`方法。

例如，我们可以写:

```
const obj = {
  foo: 1,
  bar: 2
}
const newObj = Object.assign({}, obj, {
  baz: 3
})
console.log(newObj)
```

我们有一个需要添加`baz`属性的`obj`。

为此，我们用一个空对象[、`obj`和一个属性为`baz`的对象来调用`Object.assign`。](https://differ.plainenglish.io/p/how-to-check-for-an-empty-object-in-javascript-dvjxdkyal)

然后将第二个和第三个参数中对象的所有属性放入空对象并返回。

因此，`newObj`就是:

```
{
  "foo": 1,
  "bar": 2,
  "baz": 3
}
```

# 使用扩展运算符

将属性添加到对象中的另一种方法是使用 spread 运算符。

例如，我们可以写:

```
const obj = {
  foo: 1,
  bar: 2
}
const newObj = {
  ...obj,
  baz: 3
}
console.log(newObj)
```

我们将`obj`的属性展开到`newObj`中。

然后我们把`baz`属性放在那之后。

因此，`newObj`是:

```
{
  "foo": 1,
  "bar": 2,
  "baz": 3
}
```

# 结论

我们可以使用`Object.assign`方法或 spread 操作符向对象添加一个属性。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*