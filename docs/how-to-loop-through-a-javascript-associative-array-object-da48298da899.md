# 如何遍历一个 JavaScript 关联数组对象？

> 原文：<https://javascript.plainenglish.io/how-to-loop-through-a-javascript-associative-array-object-da48298da899?source=collection_archive---------2----------------------->

![](img/77399227b944925f7ca3d42d492be8ea.png)

Photo by [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在 JavaScript 代码中循环遍历 JavaScript 关联数组对象。

在本文中，我们将研究如何遍历 JavaScript 关联数组对象。

# 使用 for-in 循环

使用`for-in`循环遍历 JavaScript 关联数组对象的一种方法。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}
for (const key in obj) {
  const value = obj[key];
  console.log(key, value);
}
```

我们用一些键值对创建了一个`obj`对象。

然后我们用`for-in`循环遍历对象键。

我们用循环体中的`obj[key]`获得属性值。

因此，从控制台日志中，我们得到:

```
a 1
b 2
c 3
```

# 将 Object.entries 与 forEach 方法一起使用

我们可以使用`Object.entries`方法返回一个键值对数组。

然后我们可以使用`forEach`方法来遍历数组。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}
Object.entries(obj).forEach(([key, value]) => console.log(key, value));
```

我们用一个回调函数调用`forEach`,回调函数包含一个数组，数组中的`key`和`value`被析构。

然后在回调体中，我们记录了`key`和`value`。

因此，我们得到和以前一样的结果。

# 使用 for-of 循环

另一种遍历键值对的方法是使用`for-of`循环。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}for (const [key, value] of Object.entries(obj)) {
  console.log(key, value)
}
```

我们使用`Object.entries`返回一个键值对数组。

我们从析构的键-值数组中析构键和值。

我们从控制台日志中记录`key`和`value`。

# 结论

有几种方法可以用 JavaScript 遍历关联数组对象的键值对。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*