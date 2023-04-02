# 如何从一个 JavaScript 数组的所有元素中筛选出另一个数组？

> 原文：<https://javascript.plainenglish.io/how-to-filter-a-javascript-array-from-all-elements-of-another-array-c71e2039f8d4?source=collection_archive---------8----------------------->

![](img/3e0f4d6b9b8925a2c68a46864cef73ac.png)

Photo by [Raychan](https://unsplash.com/@wx1993?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望从一个 JavaScript 数组的所有元素中过滤出另一个 JavaScript 数组。

在本文中，我们将研究如何从一个 JavaScript 数组的所有元素中过滤出另一个数组。

# 使用 Array.prototype.filter 方法

我们可以使用 JavaScript array `filter`方法过滤掉作为另一个数组条目的数组条目。

例如，我们可以写:

```
const filtered = [1, 2, 3, 4].filter(
  function(e) {
    return this.indexOf(e) < 0;
  },
  [2, 4]
);
console.log(filtered);
```

这样做。

我们通过调用`this.indexOf(e) < 0`并返回结果的回调来调用`[1, 2, 3, 4]`上的`filter`。

我们在回调中用第二个参数`filter`设置`this`的值。

所以，`this`就是`[2, 4]`。

所以`filtered`就是`[1, 3]`。

我们还可以使用`includes`方法来过滤掉其他数组中的项目。

例如，我们可以写:

```
const filtered = [1, 2, 3, 4].filter(
  function(e) {
    return !this.includes(e);
  },
  [2, 4]
);
console.log(filtered);
```

对于`filter`，我们得到了相同的结果。

如果在回调函数中不使用`this`，我们可以用数组函数替换回调函数。

为此，我们可以写:

```
const filtered = [1, 2, 3, 4].filter(
  (e) => {
    return [2, 4].indexOf(e) < 0;
  }
);
console.log(filtered);
```

或者:

```
const filtered = [1, 2, 3, 4].filter(
  (e) => {
    return ![2, 4].includes(e);
  }
);
console.log(filtered);
```

我们用数组本身替换`this`。

我们得到了同样的结果。

# 结论

我们可以使用 JavaScript array `filter`实例方法返回一个数组，该数组过滤掉了包含在另一个数组中的项目。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*