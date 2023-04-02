# 如何用 JavaScript 从一个日期中减去 6 个月

> 原文：<https://javascript.plainenglish.io/javascript-subtract-6-months-from-date-2fc1c384be04?source=collection_archive---------9----------------------->

## 一个关于如何用 JavaScript 从一个日期中轻松减去 6 个月的教程。

![](img/397d6ffd19666d89452bd9d93ec72928.png)

要从日期中减去 6 个月:

1.  在日期上调用`getMonth()`方法来获取月份。
2.  从`getMonth()`的返回值中减去 6。
3.  将减法的结果传递给`setMonth()`方法。

例如:

```
function subtract6Months(date) {
  date.setMonth(date.getMonth() - 6); return date;
}// November 14, 2022
const date = new Date('2022-11-14T00:00:00.000Z');const newDate = subtract6Months(date);// May 14, 2022
console.log(newDate); // 2022-05-14T00:00:00.000Z
```

我们的`subtract6Months()`函数将一个`Date`对象和要减去的月数作为参数。它返回减去 6 个月的同一个`Date`对象。

Date getMonth()返回一个从零开始的数字，表示特定日期的月份。

Date setMonth()方法将日期的月份设置为指定的从零开始的数字。

**注:**此处的“零基”是指`0`为一月、`1`为二月、`2`为三月等。

如果减去的月份会减少日期的年份，`setMonths()`将自动更新日期信息以反映这一点。

```
// January 10, 2022
const date = new Date('2022-01-10T00:00:00.000Z');date.setMonth(date.getMonth() - 6);// July 10, 2021
console.log(date); // 2021-07-10T00:00:00.000Z
```

在本例中，我们从 2022 年 1 月的日期中减去 6 个月。这使得年份自动回滚到 2021 年`setMonth()`。

## 避免副作用

`setMonth()`改变了它所调用的`Date`对象。这给我们的`subtract6Months()`函数带来了副作用。为了避免修改传递的`Date`并创建一个纯函数，制作一个`Date`的副本并在这个副本上调用`setMonth()`，而不是原始的。

```
function subtract6Months(date) {
  // 👇 Make copy with "Date" constructor
  const dateCopy = new Date(date); dateCopy.setMonth(dateCopy.getMonth() - 6); return dateCopy;
}// August 13, 2022
const date = new Date('2022-08-13T00:00:00.000Z');const newDate = subtract6Months(date);// February 13, 2022
console.log(newDate); // 2022-02-13T00:00:00.000Z// 👇 Original not modified
console.log(date); // 2022-08-13T00:00:00.000Z
```

**提示:**不修改外部状态的函数(即纯函数)往往更容易预测，也更容易推理，因为它们对于特定的输入总是给出相同的输出。这使得限制代码中副作用的数量成为一个很好的实践。

# 2.日期-fns `subMonths()`功能

或者，我们可以使用 [date-fns](https://www.npmjs.com/package/date-fns) NPM 包中的`subMonths()`函数快速从一个日期中减去 6 个月。它像我们的纯`subtractMonths()`函数一样工作。`subMonths()`接受一个`Date`对象和要减去的月数作为参数。它返回一个减去月份的新的`Date`对象。

```
import { subMonths } from 'date-fns';// July 26, 2022
const date = new Date('2022-07-26T00:00:00.000Z');const newDate = subMonths(date, 6);// January 26, 2022
console.log(newDate); // 2022-01-26T00:00:00.000Z// Original not modified
console.log(date); // 2022-07-26T00:00:00.000Z
```

注意，`subMonths()`函数返回一个新的`Date`对象，而不修改传递给它的对象。

*原载于*【codingbeautydev.com】

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*