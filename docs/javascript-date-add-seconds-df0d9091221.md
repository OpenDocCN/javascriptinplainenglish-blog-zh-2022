# 如何在 JavaScript 中轻松地给日期添加秒数

> 原文：<https://javascript.plainenglish.io/javascript-date-add-seconds-df0d9091221?source=collection_archive---------12----------------------->

![](img/95c7519a559c2b76dbd320403a655b48.png)

# 1.Date setSeconds()和 getSeconds()方法

要在 JavaScript 中给日期添加秒，使用`getSeconds()`方法获取秒，然后对日期调用`setSeconds()`方法，将`getSeconds()`和要添加的秒数之和作为参数传递。

例如:

```
function addSeconds(date, seconds) {
  date.setSeconds(date.getSeconds() + seconds);
  return date;
}// 12:00:00 AM on April 17, 2022
const date = new Date('2022-04-17T00:00:00.000Z');// 12:00:20 AM on April 17, 2022
const newDate = addSeconds(date, 20);console.log(newDate); // 2022-04-17T00:00:20.000Z
```

我们的`addSeconds()`函数接受一个`Date`对象和要添加的秒作为参数。它返回一个新的`Date`对象和新添加的秒数。

[Date getSeconds()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getSeconds) 方法返回一个 0 到 59 之间的数字，表示特定日期的秒数。

[Date setSeconds()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/setSeconds) 将日期的秒数设置为指定的数字。

如果增加的秒数会增加`Date`的分钟、小时、日或年，`setSeconds()`会自动更新`Date`信息以反映这一点。

```
// 12:00:00 AM on April 17, 2022
const date = new Date('2022-04-17T00:00:00.000Z');// Add 100 seconds to date
date.setSeconds(date.getSeconds() + 100);// 12:01:40 AM on April 17, 2022
console.log(date); // 2022-04-17T00:01:40.000Z
```

在本例中，将`100`传递到`setSeconds()`会将日期的分钟数增加`1` (60 秒)，并将秒数设置为`40`。

## 避免副作用

`setSeconds()`方法改变了它所调用的`Date`对象。这给我们的`addSeconds()`函数带来了副作用。为了避免修改过去的日期并创建一个纯函数，制作日期的副本并在该副本上调用`setSeconds()`,而不是原始的:

```
function addSeconds(date, seconds) {
  // Making a copy with the Date() constructor
  const dateCopy = new Date(date);
  dateCopy.setSeconds(date.getSeconds() + seconds);return dateCopy;
}const date = new Date('2022-04-17T00:00:00.000Z');const newDate = addSeconds(date, 20);
console.log(newDate); // 2022-04-17T00:00:20.000Z// Original not modified
console.log(date); // 2022-04-17T00:00:00.000Z
```

## 小费

不修改外部状态的函数(即纯函数)更容易预测，也更容易推理。这使得限制程序中副作用的数量成为一个好习惯。

# 2.日期-fns 添加秒()

或者，您可以使用来自`date-fns` NPM 包的纯`addSeconds()`函数，在 JavaScript 中快速给日期添加秒数。

```
import { addSeconds } from 'date-fns';const date = new Date('2022-04-17T00:00:00.000Z');const newDate = addSeconds(date, 20);
console.log(newDate); // 2022-04-17T00:00:20.000Z// Original not modified
console.log(date); // 2022-04-17T00:00:00.000Z
```

*最初发表于:*[*codingbeautydev.com*](https://cbdev.link/1ffa53)

# ES13 中 11 个惊人的新 JavaScript 特性

本指南将带您快速了解 ECMAScript 13 中添加的所有最新功能。这些强大的新特性将会用更短、更富于表现力的代码来更新您的 JavaScript。

![](img/75a56482761ab63cfc081ad691d70d61.png)

[注册](https://cbdev.link/900477)，立即免费领取一份。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。******