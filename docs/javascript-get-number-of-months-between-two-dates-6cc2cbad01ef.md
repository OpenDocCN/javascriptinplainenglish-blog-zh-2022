# 如何在 JavaScript 中获得两个日期之间的月数

> 原文：<https://javascript.plainenglish.io/javascript-get-number-of-months-between-two-dates-6cc2cbad01ef?source=collection_archive---------14----------------------->

![](img/bafd7f8b9d8b835ff3ba26bd5b9dd9ed.png)

# 1.`Date` `getMonth()`法

要在 JavaScript 中获取两个日期之间的月数:

1.  使用`date1.getMonth() - date2.getMonth()`获得两个日期之间的月份差异。
2.  使用`date1.getYear() - date2.getYear()`获得两个日期之间的差异。
3.  将月份差加上年份差乘以 12，即`monthDiff + yearDiff * 12`。

例如:

```
function differenceInMonths(date1, date2) {
  const monthDiff = date1.getMonth() - date2.getMonth();
  const yearDiff = date1.getYear() - date2.getYear();

  return monthDiff + yearDiff * 12;
}

// June 5, 2022
const date1 = new Date('2022-06-05');

// March 17, 2021
const date2 = new Date('2021-03-17');

const difference = differenceInMonths(date1, date2);

console.log(difference); // 15
```

我们可重用的`differenceInMonths()`函数接受两个`Date`对象，并返回它们之间的月差。第一个参数是开始日期，第二个参数是结束日期。

`[Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getMonth)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getMonth)`[getMonth()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getMonth)`方法返回一个从零开始的数字，表示特定日期的月份。

**注:**这里的“零基”是指`0`是一月，`1`是二月，`2`是三月等等。

除了减去月份，我们还需要减去年份，因为两个日期可能有不同的年份，这当然会影响它们之间的月数。我们使用`getFullYear()`方法获得日期的年份并减去它们。

`[Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear)`[getFullYear()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear)`方法返回一个表示特定日期的年份的数字。

一年等于 12 个月，所以在得到年差之后，我们用它乘以 12 得到相等的月，然后把它加到月差上。

# 2.`date-fns` `differenceInMonths()`功能

或者，我们可以使用`[date-fns](https://www.npmjs.com/package/date-fns)` NPM 包中的`differenceInMonths()`函数来快速获得 JavaScript 中两个日期之间的月差。它的工作方式就像我们自己的`differenceInMonths()`函数一样，接受两个`Date`对象并返回它们的月份差。

```
import { differenceInMonths } from 'date-fns';

const date1 = new Date('2022-08-10');

const date2 = new Date('2020-02-24');

const difference = differenceInMonths(date1, date2);

console.log(difference); // 29
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/36c21c)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费周报**](http://newsletter.plainenglish.io/) 。关注我们 [**推特**](https://twitter.com/inPlainEngHQ) ，[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**，**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**，以及** [**不和谐**](https://discord.gg/GtDtUAvyhW) **。**

## 想用内容来扩展你的科技创业吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。