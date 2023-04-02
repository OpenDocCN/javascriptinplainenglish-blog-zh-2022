# 如何在 JavaScript 中检查一个数字是 NaN？

> 原文：<https://javascript.plainenglish.io/how-to-check-that-a-number-is-nan-in-javascript-792a276f1aee?source=collection_archive---------18----------------------->

![](img/4765901ae9fb62013011a34fc85f6f7f.png)

Photo by [NeONBRAND](https://unsplash.com/@neonbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获取独家写作机会和建议。*

有时，我们可能想在 JavaScript 中检查一个数字是否为`NaN`。

在本文中，我们将看看在 JavaScript 中检查数字是否为`NaN`的方法。

# `The isNaN Function`

我们可以使用`isNaN`函数来检查一个数字是否是`NaN`。

例如，我们可以写:

```
const nan = isNaN(parseFloat("abc"))
console.log(nan)
```

`isNaN`将尝试把我们传递给它的参数自动解析为一个数字。

但是为了安全起见，我们可以先用`parseFloat`自己解析它，以确保得到预期的结果。

我们`parseFloat`应该返回`NaN`，因为我们向它传递了一个非数字字符串。

所以`isNaN`应该返回`NaN`。

所以，`nan`就是`true`。

# 检查一个值是否等于它本身

由于`NaN`是 JavaScript 中唯一不等于自身的值，我们可以检查变量是否等于自身，以检查变量的值是否为`NaN`。

例如，我们可以写:

```
const nan = NaN
console.log(nan !== nan)
```

然后控制台日志将显示`true`，因为`NaN`不等于自身。

如果`nan`有任何其他值，控制台日志将记录`false`。

所以如果我们有:

```
const nan = true
console.log(nan !== nan)
```

然后控制台日志会显示`false`。

# `The Number.isNaN Method`

`Number.isNaN`方法是另一个让我们检查传递给它的值是否是`NaN`的方法。

`isNaN`和`Number.isNaN`的区别在于`Number.isNaN`在检查之前不会尝试将值转换成数字。

例如，我们可以写:

```
const nan = Number.isNaN('abc');
console.log(nan)
```

然后控制台日志显示`false`，因为我们没有传入`NaN`。

我们刚刚传入了一个不是数字的东西。

但是如果我们写:

```
const nan = Number.isNaN(NaN);
console.log(nan)
```

那么`nan`就是`true`。

# `Object.is`

我们可以用来检查`NaN`的另一种方法是`Object.is`方法。

`Object.is`接受两个参数和我们想要比较的值。

如果两个值都是`NaN`，那么它返回`true`而不是`false`，就像我们使用`===`一样。

例如，我们可以写:

```
const a = NaN
const nan = Object.is(a, NaN);
console.log(nan)
```

然后`nan`根据控制台日志就是`true`。

# 结论

我们可以用 JavaScript 提供的各种函数和方法来检查`NaN`。

同样，我们可以使用`===`操作符来检查一个值是否不等于它本身。

如果不相等，那么我们知道值必须是`NaN`，因为`NaN`是 JavaScript 中唯一不等于自身的值。