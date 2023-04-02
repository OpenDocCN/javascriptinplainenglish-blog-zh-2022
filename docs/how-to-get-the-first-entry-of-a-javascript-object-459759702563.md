# 如何获取一个 JavaScript 对象的第一个入口？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-first-entry-of-a-javascript-object-459759702563?source=collection_archive---------6----------------------->

![](img/e29871ac6c0cd93ca8711dee3631ddb8.png)

Photo by [Kyle Glenn](https://unsplash.com/@kylejglenn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要获取 JavaScript 对象的第一个条目。

在本文中，我们将研究如何获取 JavaScript 对象的第一个条目。

# 对象.键

我们可以使用`Object.keys`方法返回一个对象键数组。

因此，我们可以用它来获取第一个对象属性的键名。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
};
console.log(Object.keys(obj)[0])
```

我们有返回`'a'`的`Object.keys(obj)[0]`，因为它是`obj`中的第一个条目。

# 对象.值

我们可以使用`Object.values`方法返回一个对象属性值数组。

因此，我们可以用它来获取第一个对象属性的值。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
};
console.log(Object.values(obj)[0])
```

我们有返回 1 的`Object.values(obj)[0]`，因为它是`obj`中第一个条目的值。

# 对象.条目

我们可以使用`Object.entries`方法返回一个对象中键值对的数组。

因此，我们可以用它来获得第一个对象属性的键值对。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
};
console.log(Object.entries(obj)[0])
```

我们有返回`[“a”, 1]`的`Object.entries(obj)[0]`，因为它是`obj`中的第一个键值对。

# 洛达什托皮斯法

Lodash `toPairs`方法的作用与`Object.entries`相同。

因此，如果`Object.entries`不可用，我们可以使用它。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
};
console.log(_.toPairs(obj)[0])
```

我们在控制台日志中得到结果`[“a”, 1]`。

# 结论

我们可以用普通的 JavaScript 或 Lodash 获取一个 JavaScript 对象的第一个条目。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*