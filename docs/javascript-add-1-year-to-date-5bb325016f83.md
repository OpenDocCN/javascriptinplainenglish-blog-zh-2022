# 如何在 JavaScript 中给日期加上 1 年

> 原文：<https://javascript.plainenglish.io/javascript-add-1-year-to-date-5bb325016f83?source=collection_archive---------2----------------------->

## 了解在 JavaScript 中轻松添加 1 年至今对象的多种方法。

![](img/d7f6f8fe06be5038503a89d13a7b9fd9.png)

让我们来看看在 JavaScript 中给一个`Date`对象添加 1 年的一些方法。

# 1.Date setFullYear()和 getFullYear()方法

要给日期加上 1 年，调用日期上的`getFullYear(`方法得到年份，然后调用日期上的`setFullYear()`方法，传递`getFullYear()`和`1`之和作为参数，即`date.setFullYear(date.getFullYear() + 1)`。

例如:

```
function addOneYear(date) {
  date.setFullYear(date.getFullYear() + 1);
  return date;
}// April 20, 2022
const date = new Date('2022-04-20T00:00:00.000Z');const newDate = addOneYear(date);// April 20, 2023
console.log(newDate); // 2023-04-20T00:00:00.000Z
```

我们的`addOneYear()`函数接受一个`Date`对象，并返回相同的`Date`，其中年份增加 1。

`Date` `getFullYear()`方法返回一个表示特定日期的年份的数字。

`Date` `setFullYear()`方法将日期的年份设置为一个指定的数字。

## 避免副作用

`setFullYear()`方法改变了它所调用的`Date`对象。这在我们的`addOneYear()`函数中引入了一个[副作用](https://en.wikipedia.org/wiki/Side_effect_(computer_science))。为了避免修改传递的`Date`并创建一个纯函数，制作一个`Date`的副本并在这个副本上调用`setFullYear()`，而不是原始的。

```
function addOneYear(date) {
  // Making a copy with the Date() constructor
  const dateCopy = new Date(date); dateCopy.setFullYear(dateCopy.getFullYear() + 1); return dateCopy;
}// April 20, 2022
const date = new Date('2022-04-20T00:00:00.000Z');const newDate = addOneYear(date);// April 20, 2023
console.log(newDate); // 2023-04-20T00:00:00.000Z// Original not modified
console.log(date); // 2022-04-20T00:00:00.000Z
```

不修改外部状态的函数(即纯函数)更容易预测，也更容易推理。这使得限制程序中副作用的数量成为一个好习惯。

# 2.date-fns addYears()函数

或者，我们可以使用 [date-fns](https://www.npmjs.com/package/date-fns) NPM 包中的纯`addYears()`函数快速地将一年加到一个日期上。

```
import { addYears } from 'date-fns';// April 20, 2022
const date = new Date('2022-04-20T00:00:00.000Z');const newDate = addYears(date, 1);// April 20, 2023
console.log(newDate); // 2023-04-20T00:00:00.000Z// Original not modified
console.log(date); // 2022-04-20T00:00:00.000Z
```

该函数将一个`Date`对象和要添加的年数作为参数，并返回一个新的带有新添加的年数的`Date`对象。它不会修改传递给它的原始日期。

*更新于:*[*codingbeautydev.com*](https://cbdev.link/5959a4)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。