# 如何有条件地给 JavaScript 对象添加成员？

> 原文：<https://javascript.plainenglish.io/how-to-conditionally-add-a-member-to-a-javascript-object-bfa8765e411f?source=collection_archive---------8----------------------->

![](img/fea05aeece4d95b3fc12da0a65d44536.png)

Photo by [Sonja Langford](https://unsplash.com/@sonjalangford?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望有条件地向 JavaScript 对象添加成员。

在本文中，我们将了解如何有条件地向 JavaScript 对象添加成员。

# 传播算子

我们可以使用 spread 运算符有条件地将一个对象扩展到另一个对象中。

例如，我们可以写:

```
const condition = true
const obj = {
  ...(condition && {
    b: 5
  })
}
console.log(obj)
```

只有当`condition`是`true`时，我们才使用`&&`操作符返回对象。

如果对象被返回，那么它将被传播到`obj`。

所以我们得到:

```
{b: 5}
```

结果。

除了使用`&&`运算符，我们还可以通过编写以下代码来使用三元运算符:

```
const condition = true
const obj = {
  ...(condition ? {
    b: 5
  } : {})
}
console.log(obj)
```

当`condition`是`false`而不是`null`时，我们返回一个空对象。

# 对象.分配

同样，我们可以使用`Object.assign`方法将一个对象合并到另一个对象中。

例如，我们可以写:

```
const condition = true
const obj = Object.assign({}, condition ? {
  b: 5
} : null)
console.log(obj)
```

我们在`Object.assign`方法的第二个参数中有`condition`检查。

只有当`condition`为`true`时，我们才返回对象。

否则，返回`null`。

由于`condition`是`true`，我们对`obj`也有同样的结果。

# 结论

我们可以用 spread 操作符或`Object.assign`方法有条件地给一个对象添加属性。

我们可以使用三元运算符或`&&`运算符来指定给定条件下要添加的内容。

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*