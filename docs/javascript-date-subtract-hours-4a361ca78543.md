# 如何在 JavaScript 中从日期中减去小时

> 原文：<https://javascript.plainenglish.io/javascript-date-subtract-hours-4a361ca78543?source=collection_archive---------7----------------------->

## 了解在 JavaScript 中从日期对象中轻松减去任意小时数的多种方法

![](img/071fec1b0a25e98b2149579e0360dab1.png)

让我们看看在 JavaScript 中从`Date`对象中减去任意小时数的方法。

# 1.日期设置小时()和获取小时()方法

从`Date`中减去小时:

1.  调用`Date`上的`getHours()`方法获取小时数。
2.  减去小时数。
3.  将减法的结果传给`setHours()`法。

```
function subtractHours(date, hours) {
  date.setHours(date.getHours() - hours); return date;
}// 8 AM on June 20, 2022
const date = new Date('2022-06-20T08:00:00.000Z');const newDate = subtractHours(date, 2);// 6 AM on June 20, 2022
console.log(date); // 2022-06-20T06:00:00.000Z
```

我们的`subtractHours()`函数以`Date`对象和要减去的小时数作为参数。它返回相同的`Date`对象，并减去小时。

日期 [getHours()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getHours) 方法返回一个介于`0`和`23`之间的数字，代表特定日期的小时数。

日期[设置小时()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/setHours)方法将`Date`的小时设置为指定的数字。

如果我们减去的小时会减少`Date`的日、月或年，`setHours()`会自动更新`Date`信息以反映这一点。

```
// 12 AM on June 20, 2022
const date = new Date('2022-06-20T00:00:00.000Z');date.setHours(date.getHours() - 3);// 9 PM on June 19, 2022 (previous day)
console.log(date); // 2022-06-19T21:00:00.000Z
```

在本例中，将`Date`的小时数减少`3`会将一天的小时数减少 1，并将小时数设置为`21`。

## 避免副作用

`setHours()`方法对它所调用的`Date`对象进行变异。这会给我们的`subtractHours()`功能带来副作用。为了避免修改经过的日期并创建一个纯函数，制作一个日期的副本并在该副本上调用`setHours()`，而不是原始日期:

```
function subtractHours(date, hours) {
  const dateCopy = new Date(date); dateCopy.setHours(dateCopy.getHours() - hours); return date;
}// 8 AM on June 20, 2022
const date = new Date('2022-06-20T08:00:00.000Z');const newDate = subtractHours(date, 2);// 6 AM on June 20, 2022
console.log(date); // 2022-06-20T06:00:00.000Z// Original not modified
console.log(newDate); // 2022-06-20T08:00:00.000Z
```

**提示:**不改变外部状态的函数(即纯函数)更容易预测和推理。这使得限制代码中副作用的数量成为一种良好的做法。

# 2.日期-fns 子小时()函数

或者，我们可以使用 [date-fns](https://www.npmjs.com/package/date-fns) NPM 包中的`subHours()`函数，从`Date`中快速减去小时。它的工作原理类似于我们的纯`subtractHours()`函数。

```
import { subHours } from 'date-fns';// 8 AM on June 20, 2022
const date = new Date('2022-06-20T08:00:00.000Z');const newDate = subHours(date, 2);// 6 AM on June 20, 2022
console.log(date); // 2022-06-20T06:00:00.000Z// Original not modified
console.log(newDate); // 2022-06-20T08:00:00.000Z
```

*原载于*[](https://cbdev.link/c3cb44)

# *ES13 中 11 个惊人的新 JavaScript 特性*

*本指南将带您了解 ECMAScript 13 中添加的所有最新功能。这些强大的新特性将会用更短、更富于表现力的代码来更新您的 JavaScript。*

*![](img/75a56482761ab63cfc081ad691d70d61.png)*

*[报名](https://cbdev.link/900477)立即免费领取一份。*