# 如何在 JavaScript 中从月份名中获取月份号

> 原文：<https://javascript.plainenglish.io/javascript-get-number-from-name-a00ba2ed9027?source=collection_archive---------10----------------------->

![](img/cf0186e2a1cad4fd73614124e4a01a34.png)

在本文中，我们将学习如何使用 JavaScript 从名称中获取一个月在 12 个月列表中的位置。也就是说，我们将从`January`得到`1`，从`February`得到`2`，从`March`得到`3`，以此类推。

为此，根据名称创建一个日期字符串，并将该字符串传递给`Date()`构造函数。然后使用`getMonth()`方法获得月份号。例如:

```
function getMonthNumberFromName(monthName) {
  return new Date(`${monthName} 1, 2022`).getMonth() + 1;
}console.log(getMonthNumberFromName('January')); // 1
console.log(getMonthNumberFromName('February')); // 2
console.log(getMonthNumberFromName('March')); // 3
```

我们将月份插入到一个字符串中，这个字符串可以被`Date()`构造函数解析以创建一个新的`Date`对象。然后我们使用`getMonth()`方法获得日期的月份。

`getMonth()`方法返回一个从零开始的月份索引，即`0`表示`January`，`1`表示`February`，`2`表示`March`等等。

```
const month1 = new Date('January 1, 2022').getMonth();
console.log(month1); // 0const month2 = new Date('February 1, 2022').getMonth();
console.log(month2); // 1
```

这就是为什么我们把`1`加到它上面并返回结果的原因。

我们的函数也适用于缩写的月份名称，因为`Date()`构造函数也可以用它们解析日期字符串。

```
function getMonthNumberFromName(monthName) {
  return new Date(`${monthName} 1, 2022`).getMonth() + 1;
}console.log(getMonthNumberFromName('Jan')); // 1
console.log(getMonthNumberFromName('Feb')); // 2
console.log(getMonthNumberFromName('Mar')); // 3
```

如果月份名称使得结果日期字符串无法被`Date()`构造函数解析，那么将会创建一个无效的日期，`getMonth()`将返回`NaN`。

```
const date = new Date('Invalid 1, 2022');console.log(date); // Invalid Date
console.log(date.getMonth()); // NaN
```

这意味着我们的函数也将返回`NaN`:

```
function getMonthNumberFromName(monthName) {
  return new Date(`${monthName} 1, 2022`).getMonth() + 1;
}console.log(getMonthNumberFromName('Invalid')); // NaN
```

如果我们返回`-1`可能会更好。我们可以使用`isNaN()`功能检查无效日期。

```
function getMonthNumberFromName(monthName) {
  const date = new Date(`${monthName} 1, 2022`); if (isNaN(date)) return -1; return date.getMonth() + 1;
}console.log(getMonthNumberFromName('Invalid')); // -1
```

或者，我们可以从函数中抛出一个错误:

```
function getMonthNumberFromName(monthName) {
  const date = new Date(`${monthName} 1, 2022`); if (isNaN(date)) {
    throw new Error('Invalid month name.');
  } return date.getMonth() + 1;
}// Error: Invalid month name.
console.log(getMonthNumberFromName('Invalid'));
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/362e3b)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。