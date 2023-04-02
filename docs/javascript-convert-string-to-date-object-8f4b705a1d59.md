# 如何在 JavaScript 中将字符串转换成日期对象

> 原文：<https://javascript.plainenglish.io/javascript-convert-string-to-date-object-8f4b705a1d59?source=collection_archive---------10----------------------->

## 了解如何在 JavaScript 中轻松地将字符串转换为日期对象。

![](img/b02d0a739c8eb5fd104924ad31944b59.png)

# 1.Date()构造函数

要将字符串转换为日期对象，调用`Date()`构造函数，将字符串作为参数传递，即`const date = new Date(str)`。例如:

```
const str = '2022-06-15';const date = new Date(str);console.log(date.getFullYear()); // 2022
console.log(date.getDate()); // 15
console.log(date); // 2022-06-15T00:00:00.000Z
```

如果传递了一个字符串，`Date()`构造函数从字符串中的信息创建一个`Date`对象。

## 无效日期

如果传递的字符串具有错误或不支持的格式，将会抛出错误或创建无效日期，具体取决于实现。例如:

```
const invalidDate = new Date('a');
console.log(invalidDate); // Invalid Dateconst invalidDate2 = new Date('15/6/2022');
console.log(invalidDate2); // Invalid Date
```

## 如何将非 ISO-8601 格式的字符串转换为日期对象

确保传递给`Date()`构造函数的字符串符合 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 格式(`YYYY-MM-DDTHH:mm:ss.sssZ`)对于跨所有浏览器的一致解析行为很重要。其他格式的解析行为取决于实现，并且可能不适用于所有浏览器。

为了转换非 ISO 8601 格式的字符串并保持一致的解析行为，我们可以从字符串中获取各个日期组件值，并将它们作为数字传递给`Date()`构造函数。例如，我们可以将一个带有`MM/DD/YY`格式的字符串转换成一个`Date`对象，如下所示:

```
const str = '06/15/2022';const [month, day, year] = str.split('/');console.log(month); // 06
console.log(day); // 15
console.log(year); // 2022const date = new Date(+year, +month - 1, +day);
console.log(date); // May 15, 2022
```

我们使用`String` `split()`方法用正斜杠(`/`)分割字符串，以获得月、日和年的各个值。我们用一元运算符(`+`)将它们转换成数字，并将其传递给`Date()`构造函数。

**注意:**在将月份传递给`Date()`构造函数时，我们从月份中减去了`1`，因为`Date()`需要一个从零开始的月份值，即 0 =一月，1 =二月，2 =三月，等等。

当在字符串中指定时间时，我们可以采用类似的方法。在下面的示例中，我们转换的字符串指定了小时、分钟和秒。

```
const str = '06-15-2022 09:13:50';const [dateStr, timeStr] = str.split(' ');
console.log(dateStr); // 06-15-2022
console.log(timeStr); // 09:13:50const [month, day, year] = dateStr.split('-');
const [hours, minutes, seconds] = timeStr.split(':');console.log(month); // 06
console.log(day); // 15
console.log(year); // 2022const date = new Date(
  +year,
  +month - 1,
  +day,
  +hours,
  +minutes,
  +seconds
);
console.log(date); // 2022-06-15T08:13:50.000Z
```

首先，我们必须用空格将字符串分开，以便分别使用日期和时间字符串。

与上一个例子不同，这次日期字符串中的值用连字符(`-`)分隔，所以我们在调用`split()`来分别获取月、日和年时使用它作为分隔符。

类似地，时间字符串中的值用冒号(`:`)分隔，所以这是我们用`String` `split()`方法分隔它们的分隔符。

在分别获得每个日期和时间值后，我们用一元运算符(`+`)将它们转换成数字，并将其传递给`Date()`构造函数。

## 如何将日期对象转换为 ISO 8601 字符串

如果我们想将一个`Date`对象转换成一个字符串以存储在一个文件或数据库中，我们可以以 ISO 8601 格式存储它，这样我们就可以检索并轻松地将其转换回一个具有独立于浏览器的解析行为的`Date`对象，而无需使用任何第三方库。

我们可以用`toISOString()`方法来做这件事。

```
const str = '06-15-2022 09:13:50';const [dateStr, timeStr] = str.split(' ');
console.log(dateStr); // 06-15-2022
console.log(timeStr); // 09:13:50const [month, day, year] = dateStr.split('-');
const [hours, minutes, seconds] = timeStr.split(':');console.log(month); // 06
console.log(day); // 15
console.log(year); // 2022const date = new Date(
  +year,
  +month - 1,
  +day,
  +hours,
  +minutes,
  +seconds
);const isoString = date.toISOString();
console.log(isoString); // 2022-06-15T08:13:50.000Z// Can convert back to Date object with browser-independent parsing
const sameDate = new Date(isoString);
console.log(sameDate.getDate()); // 15
console.log(sameDate.getMinutes()); // 13
```

`Date` `toISOString()`方法根据世界时返回一个 ISO 8601 格式的日期字符串。

# 2.date-fns parse()函数

我们还可以使用`date-fns` NPM 包中的 [parse()](https://date-fns.org/v2.16.1/docs/parse) 函数，轻松地将各种格式的字符串转换成`Date`对象。这里我们指定字符串为`MM-dd-yyyy hh:m:ss` [格式](https://date-fns.org/v2.16.1/docs/format)，这样它就可以被正确转换。

```
import { parse } from 'date-fns';const str = '06-15-2022 09:13:50';const date = parse(str, 'MM-dd-yyyy hh:m:ss', new Date());console.log(date.getHours()); // 9
console.log(date.getDate()); // 15
console.log(date); // 2022-06-15T08:13:50.000Z
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/963dbb)

您可以在哪里找到我们:

🌐[网站](https://cbdev.link/b621b9) |🌟[推特](https://twitter.com/CodingBeautyDev)🌟[脸书](http://facebook.com/CodingBeautyDev)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。