# 如何获取 JavaScript 对象的属性名？

> 原文：<https://javascript.plainenglish.io/how-to-get-a-javascript-objects-property-names-281351275cd4?source=collection_archive---------8----------------------->

![](img/de09a075741d98d592d43f50b8a76560.png)

Photo by [insung yoon](https://unsplash.com/@insungyoon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想要获取 JavaScript 对象中属性的名称。

在本文中，我们将看看如何用 JavaScript 获取 JavaScript 对象的属性名。

# 使用 Object.keys 方法

我们可以使用`Object.keys`方法来返回属性名称字符串的数组。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}
Object.keys(obj).forEach(key => {
  console.log(key)
  console.log(obj[key])
})
```

我们创建了具有属性`a`、`b`和`c`的`obj`对象。

然后我们用`obj`调用`Object.keys`以字符串形式返回`obj`的属性名。

然后我们用一个回调函数调用`forEach`，这个回调函数有一个`key`参数，这个参数带有被迭代的对象的键。

在回调中，我们记录了`key`和用`obj[key]`访问的值。

因此，我们得到:

```
a
1
b
2
c
3
```

结果。

# 使用 for-in 循环

我们可以通过 for-in 循环得到对象键。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}
for (const key in obj) {
  console.log(key);
  console.log(obj[key]);
}
```

我们从`key`循环变量中获取对象键。

然后我们用同样的方法在循环体中得到键和值。

因此，我们得到:

```
a
1
b
2
c
3
```

结果就像前面的例子一样。

for-in 循环还遍历从原型对象继承的所有属性，因此我们可以获得比从`Object.keys`方法更多的键。

`Object.keys`仅从非继承属性中获取属性键。

# 结论

我们可以使用`Object.keys`方法或 for-in 循环从 JavaScript 对象中获取键。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*