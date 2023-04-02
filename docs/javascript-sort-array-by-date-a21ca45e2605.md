# 如何在 JavaScript 中按日期对对象数组进行排序

> 原文：<https://javascript.plainenglish.io/javascript-sort-array-by-date-a21ca45e2605?source=collection_archive---------1----------------------->

## 了解如何根据日期属性轻松地对 JavaScript 对象数组进行排序。

![](img/c3bb29d824902ac73fc8a67e1990fa09.png)

例如，如果我们有一个 JavaScript 对象数组，每个对象都包含一个`Date`类型的属性:

```
const events = [
  { name: 'Birthday', date: new Date('2022-04-23') },
  { name: 'Shopping', date: new Date('2022-04-17') },
  { name: 'Meeting', date: new Date('2022-04-27') },
];
```

我们如何按照`date`属性对这些对象进行排序呢？

# 数组 sort()方法

我们可以很容易地用数组`sort()`方法做到这一点:

```
events.sort((a, b) => a.date.getTime() - b.date.getTime());
```

sort 方法将回调函数作为参数。它使用该函数返回的值来决定值的排序顺序。

如果回调结果是否定的，`a`排在`b`之前。

如果结果是肯定的，`b`排在`a`之前。

如果结果是`0`，两个值的排序顺序保持不变。

这意味着我们可以轻松地按降序对数组进行排序，如下所示:

```
events.sort((a, b) => b.date.getTime() - a.date.getTime());
```

现在，当`b`大于`a`时，结果将为正，这将使`sort()`首先位于 b。

**注意:**也可以通过直接减去`Date`对象来对数组进行排序:

```
events.sort((a, b) => b.date - a.date);
```

虽然这种方法也有效，但它比用`getTime()`进行减法要慢得多。

我们对这两种方法进行了性能比较，分别用单独的`for`循环执行了 100 万次。这些是平均结果:

```
Direct subtraction: 488.675ms
Subtraction with getTime(): 196.909ms
```

# 无变异排序

`sort()`方法就地对数组进行排序，这意味着它被修改了。为了防止这种情况，我们可以使用`slice()`方法为排序创建数组的副本:

```
const sortedEvents = events.slice().sort((a, b) => a.date - b.date);
```

*更新于:*[【codingbeautydev.com】T21](https://codingbeautydev.com/blog/javascript-sort-array-by-date/)

每周获取新的 web 开发技巧和教程。

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)