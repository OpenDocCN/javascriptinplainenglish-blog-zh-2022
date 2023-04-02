# 如何在 JavaScript 中给日期添加月份

> 原文：<https://javascript.plainenglish.io/javascript-add-months-to-date-fc029f06e450?source=collection_archive---------6----------------------->

![](img/7c7b6f6627696150a3a8354a7e897dd7.png)

# 1.`Date` `getMonth()`和`setMonth()`方法

在 JavaScript 中向`Date`添加月份:

1.  调用`getMonth()`来获得月数。
2.  添加新的月份。
3.  将总和传递给`setMonth()`方法。

例如:

```
function addMonths(date, months) {
  date.setMonth(date.getMonth() + months);

  return date;
}

// May 17, 2022
const date = new Date('2022-05-17T00:00:00.000Z');

const newDate = addMonths(date, 4);

// September 17, 2022
console.log(newDate); // 2022-09-17T00:00:00.000Z
```

我们的`addMonths()`接受一个`Date`对象和要添加的月数作为参数。它返回相同的`Date`对象和新添加的月份。

`Date` `getMonth()`返回一个从零开始的数字，表示特定日期的月份。

`Date` `setMonth()`方法将日期的月份设置为指定的从零开始的数字。

**注:**此处的“零基”是指`0`为 1 月、`1`为 2 月、`2`为 3 月等。

如果添加的月份会增加`Date`的年份，`setMonth()`将自动更新`Date`对象中的信息以反映这一点。

```
// November 12, 2022
const date = new Date('2022-11-12T00:00:00.000Z');

date.setMonth(date.getMonth() + 3);

// February 12, 2023
console.log(date); // 2023-02-12T00:00:00.000Z
```

在这里，我们在 2022 年 11 月的日期上加了 3 个月。这使得`setMonth()`自动将年份更新为 2023 年。

## 避免副作用

`setMonth()`方法改变了它所调用的`Date`对象。这在我们的`addMonths()`函数中引入了一个副作用。为了避免修改传递的`Date`并创建一个纯函数，制作一个`Date`的副本并在这个副本上调用`setMonth()`，而不是原始的。

```
function addMonths(date, months) {
  // 👇 Make copy with "Date()" constructor
  const dateCopy = new Date(date);

  dateCopy.setMonth(dateCopy.getMonth() + months);
  return dateCopy;
}

// August 16, 2022
const date = new Date('2022-08-16T00:00:00.000Z');
const newDate = addMonths(date, 3);

// November 16, 2022
console.log(newDate); // 2022-11-16T00:00:00.000Z

// 👇 Original not modified
console.log(date); // 2022-08-16T00:00:00.000Z
```

**提示:**不修改外部状态的函数(即纯函数)更容易预测，也更容易推理，因为它们对于特定的输入总是给出相同的输出。这使得限制代码中副作用的数量成为一个很好的实践。

# 2.`date-fns`功能`addMonths()`

或者，我们可以使用`[date-fns](https://www.npmjs.com/package/date-fns)`库中的`addMonths()`函数快速地将月份添加到`Date`中。它的工作原理类似于我们的纯`addMonths()`函数。

```
import { addMonths } from 'date-fns';

// July 14, 2022
const date = new Date('2022-07-14T00:00:00.000Z');

const newDate = addMonths(date, 1);

// August 14, 2022
console.log(newDate); // 2022-08-14T00:00:00.000Z

// Original not modified
console.log(date); // 2022-07-14T00:00:00.000Z
```

【codingbeautydev.com】原载于[](https://cbdev.link/4f5ec6)

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*

**更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，*** *和*[****不和【T63**** *对成长黑客感兴趣？检查出*](https://discord.gg/GtDtUAvyhW) [***电路***](https://circuit.ooo/) ***。****