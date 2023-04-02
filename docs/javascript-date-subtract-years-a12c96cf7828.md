# 如何用 JavaScript 从日期中减去年份

> 原文：<https://javascript.plainenglish.io/javascript-date-subtract-years-a12c96cf7828?source=collection_archive---------10----------------------->

## 一个关于如何在 JavaScript 中从一个日期对象中轻松减去任意年数的教程。

![](img/62a788c251969caec62edf0d48d4fec4.png)

# 1.Date setFullYear()和 getFullYear()方法

用 JavaScript 从一个`Date`中减去年份:

1.  调用`Date`上的`getFullYear()`方法来获取年份。
2.  减去年份。
3.  将减法的结果传递给`setFullYear()`方法。

例如:

```
function subtractYears(date, years) {
  date.setFullYear(date.getFullYear() - years);
  return date;
}// Feb 20, 2022
const date = new Date('2022-02-20T00:00:00.000Z');const newDate = subtractYears(date, 3);// Feb 20, 2019
console.log(newDate); // 2019-02-20T00:00:00.000Z
```

我们的`subtractYears()`函数将一个`Date`对象和要减去的年数作为参数。它返回减去了年份的同一个`Date`对象。

[Date getFullYear()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear) 方法返回一个表示特定`Date`年份的数字。

方法将一个`Date`的年份设置为一个指定的数字。

## 避免副作用

`setFullYear()`方法改变了它所调用的`Date`对象。这在我们的`subtractYears()`函数中引入了一个[副作用](https://en.wikipedia.org/wiki/Side_effect_(computer_science))。为了避免修改传递的`Date`和创建一个纯函数，制作一个`Date`的副本，并在这个副本上调用`setFullYear()`，而不是原始的。

```
function subtractYears(date, years) {
  // 👇 make copy with "Date" constructor
  const dateCopy = new Date(date); dateCopy.setFullYear(date.getFullYear() - years); return dateCopy;
}const date = new Date('2022-02-20T00:00:00.000Z');const newDate = subtractYears(date, 3);// Feb 20, 2019
console.log(newDate); // 2019-02-20T00:00:00.000Z// 👇 Original not modified
console.log(date); // 2022-02-20T00:00:00.000Z
```

**提示:**不修改外部状态的函数(即纯函数)往往更容易预测，也更容易推理，因为它们对于特定的输入总是给出相同的输出。这使得限制代码中副作用的数量成为一个很好的实践。

# 2.date-fns 子年()函数

或者，我们可以使用 [date-fns](https://www.npmjs.com/package/date-fns) NPM 包中的`subYears()`函数来快速从`Date`中减去年份。它像我们的纯`subtractYears()`函数一样工作。

```
import { subYears } from 'date-fns';const date = new Date('2022-02-20T00:00:00.000Z');const newDate = subYears(date, 3);// Feb 20, 2019
console.log(newDate); // 2019-02-20T00:00:00.000Z// 👇 Original not modified
console.log(date); // 2022-02-20T00:00:00.000Z
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/82da52)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。