# 如何在 JavaScript 中给日期添加小时数

> 原文：<https://javascript.plainenglish.io/javascript-add-hours-to-date-6e3a39bb9345?source=collection_archive---------9----------------------->

## 了解在 JavaScript 中轻松向日期对象添加小时的多种方法。

![](img/2886b2d169cd2f19d26f8bafa1f086a9.png)

# 1.Date setTime()和 Date getTime()方法

要在 JavaScript 中给一个`Date`添加小时，

1.  调用`Date`上的`getTime()`方法来获取自 Unix 纪元以来的总毫秒数。
2.  在`Date`上调用`setTime()`方法，传递`getTime()`的结果和以毫秒为单位相加的小时数。

一个例子可以说明这一点:

```
function addHours(date, hours) {
  const hoursToAdd = hours * 60 * 60 * 1000;
  date.setTime(date.getTime() + hoursToAdd);
  return date;
}const date = new Date('2022-05-15T12:00:00.000Z');const newDate1 = addHours(date, 2);
console.log(newDate1); // 2022-05-15T14:00:00.000Zconst newDate2 = addHours(newDate1, 5);
console.log(newDate2); // 2022-05-15T19:00:00.000Z
```

`Date` `getTime()`方法返回 Unix 纪元和给定日期之间经过的毫秒数。Unix 纪元是 1970 年 1 月 1 日 00:00:00.000 GMT。

```
const date = new Date('2022-05-15T12:00:00.000Z'); // Milliseconds since the Unix epoch
console.log(date.getTime()); // 1652616000000
```

我们通过乘以`60 * 60 * 1000`(一小时中的毫秒数)将小时转换为毫秒。这样我们就可以将它传递给`Date` `setTime()`方法，该方法接受一个参数，该参数指定了一个特定的时间，该时间由 Unix epoch 以来的毫秒数表示。

```
// May 5, 2022 at 12:00 PM
const date = new Date('2022-05-15T12:00:00.000Z');const hours = 5;
const hoursToMs = date.getTime() + 5 * 60 * 60 * 1000;
date.setTime(hoursToMs);// May 5, 2022 at 5:00 PM
console.log(date);
```

## 注意

`setTime()`方法改变了它所调用的`Date`对象。这给我们的`addHours()`函数带来了副作用。要创建一个纯函数，创建一个`Date`的副本，并在这个副本上调用`setTime()`，而不是这个原始函数。例如:

```
function addHours(date, hours) {
  const dateCopy = new Date(date.getTime());
  const hoursToAdd = hours * 60 * 60 * 1000;
  dateCopy.setTime(date.getTime() + hoursToAdd);
  return dateCopy;
}const date = new Date('2022-05-15T12:00:00.000Z');const newDate = addHours(date, 2);
console.log(newDate); // 2022-05-15T14:00:00.000Z// Original not modified
console.log(date); // 2022-05-15T12:00:00.000Z
```

## 小费

不修改外部状态的函数(即纯函数)更容易预测，也更容易推理。

# 2.date-fns addHours()方法

或者，您可以使用`date-fns` NPM 包中的纯`addHours()`函数来快速将小时添加到`Date`中。

```
import { addHours } from 'date-fns';const date = new Date('2022-05-15T12:00:00.000Z');const newDate = addHours(date, 4);
console.log(newDate); // 2022-05-15T16:00:00.000Z// Original not modified
console.log(date); // 2022-05-15T12:00:00.000Z
```

*更新于:*【codingbeautydev.com】

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*