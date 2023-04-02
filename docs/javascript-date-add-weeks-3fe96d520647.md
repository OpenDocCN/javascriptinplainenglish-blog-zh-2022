# 如何在 JavaScript 中给日期添加周数

> 原文：<https://javascript.plainenglish.io/javascript-date-add-weeks-3fe96d520647?source=collection_archive---------1----------------------->

![](img/dfaf37bcbf36fdb7acd986bed876f96f.png)

在本文中，我们将学习如何在 JavaScript 中轻松地给一个`Date`对象添加任意周数。

# 1.Date setDate()和 getDate()方法

在 JavaScript 中将星期添加到`Date`中:

1.  使用`Date`上的`getDate()`方法获得`Date`的月份日期。
2.  将`getDate()`到`7`的结果乘以要相加的周数相加。
3.  用这个总和作为参数调用`setDate()`方法。

例如:

```
function addWeeks(date, weeks) {
  date.setDate(date.getDate() + 7 * weeks); return date;
}// May 20, 2022
const date = new Date('2022-05-20T00:00:00.000Z');const newDate = addWeeks(date, 1);// May 27, 2022
console.log(newDate); // 2022-05-27T00:00:00.000Z
```

我们的`addDays()`函数将一个`Date`对象和要添加的天数作为参数，并返回相同的`Date`对象和新添加的天数。

`Date` `getDate()`方法返回一个介于 1 和 31 之间的数字，表示特定日期是一个月中的哪一天。

`Date` `setDate()`方法将`Date`对象中的日期更改为作为参数传递的数字。

如果您指定的数字会改变`Date`的月份或年份，`setDate()`会自动更新`Date`信息以反映这一点。

```
function addWeeks(date, weeks) {
  date.setDate(date.getDate() + 7 * weeks); return date;
}// May 20, 2022
const date = new Date('2022-05-20T00:00:00.000Z');const newDate = addWeeks(date, 3);// June 10, 2022
console.log(newDate); // 2022-06-10T00:00:00.000Z
```

加 3 周加 21 天(20 + 21 = 41 天)，但 5 月只有 31 天，所以月加`1`，日设为`10` (41 - 31)。

## 避免副作用

`setDate()`方法改变了它所调用的`Date`对象。这给我们的`addDays()`函数带来了一个副作用。为了避免修改传递的`Date`并创建一个纯函数，制作一个`Date`的副本并在这个副本上调用`setDate()`，而不是原始的。

```
function addWeeks(date, weeks) {
  const dateCopy = new Date(date); dateCopy.setDate(dateCopy.getDate() + 7 * weeks); return dateCopy;
}const date = new Date('2022-05-20T00:00:00.000Z');const newDate = addWeeks(date, 3);console.log(newDate); // 2022-06-10T00:00:00.000Z// Original not modified
console.log(date); // 2022-05-20T00:00:00.000Z
```

不修改外部状态的函数(即纯函数)更容易预测，也更容易推理，因为它们对于特定的输入总是给出相同的输出。这使得限制代码中副作用的数量成为一个很好的实践。

# 2.date-fns addWeeks()函数

或者，您可以使用 [date-fns](https://www.npmjs.com/package/date-fns) NPM 包中的纯`addWeeks()`函数来快速将星期添加到`Date`中。它的工作方式类似于我们的`addWeeks()`函数。

```
import { addWeeks } from 'date-fns';const date = new Date('2022-05-20T00:00:00.000Z');const newDate = addWeeks(date, 3);console.log(newDate); // 2022-06-10T00:00:00.000Z// Original not modified
console.log(date); // 2022-05-20T00:00:00.000Z
```

*原载于*[](https://cbdev.link/1b9ae5)

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*