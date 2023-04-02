# 如何在 JavaScript 中将月份数字转换成月份名称

> 原文：<https://javascript.plainenglish.io/javascript-convert-month-number-to-name-7f1466c4d6f7?source=collection_archive---------9----------------------->

## 了解如何使用 JavaScript 通过月份在 12 个月列表中的位置来获得月份的名称。

![](img/920265610271b134808b61c79291b553.png)

在本文中，我们将学习如何使用 JavaScript 根据月份在 12 个月列表中的位置来获取月份的名称。

# Date toLocaleString()方法

要将月份转换成月份名，创建一个具有给定月份的`Date`对象，然后使用指定的区域设置和选项调用`Date`上的`toLocaleString()`方法。

例如，下面是我们如何得到数字`1`的`January`，数字`2`的`February`，数字`March`的`3`，等等:

```
function getMonthName(monthNumber) {
  const date = new Date();
  date.setMonth(monthNumber - 1); return date.toLocaleString('en-US', { month: 'long' });
}console.log(getMonthName(1)); // January
console.log(getMonthName(2)); // February
console.log(getMonthName(3)); // March
```

我们的`getMonthName()`函数接受一个位置并返回该位置的月份名称。

方法将对象的月份设置为一个指定的数字。

## 注意

传递给`setMonth()`的值应该是从零开始的。例如，`0`代表一月，`1`代表二月，`2`代表三月，依此类推。这就是为什么我们将从月份号(`monthNumber - 1`)中减去的`1`的值传递给`setMonth()`。

我们使用 [Date toLocaleString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString) 方法来获取日期所在月份的名称。`toLocaleString()`返回一个字符串，该字符串带有日期的语言敏感表示。

该方法有两个参数:

1.  `locales`:带有 BCP 47 语言标签的字符串，或者这种字符串的数组。我们可以指定许多地区，比如`en-US`代表美国英语，`en-GB`代表英国英语，`en-CA`代表加拿大英语。
2.  `options`:用于调整日期输出格式的对象。

在我们的示例中，我们将`en-US`作为语言标签来使用美国英语，并将`long`的值设置为 options 对象的`month`属性，以显示完整的月份名称。

我们可以传递一个空数组(`[]`)作为第一个参数，让`toLocaleString()`使用浏览器的默认语言环境:

```
function getMonthName(monthNumber) {
  const date = new Date();
  date.setMonth(monthNumber - 1); // Using the browser's default locale.
  return date.toLocaleString([], { month: 'long' });
}console.log(getMonthName(1)); // January
console.log(getMonthName(2)); // February
console.log(getMonthName(3)); // March
```

这有利于国际化，因为输出会根据用户偏好的语言而变化。

我们可以为`month`属性指定除了`long`之外的其他值。例如，我们可以使用`short`将月份名称缩写成三个字母:

```
function getMonthName(monthNumber) {
  const date = new Date();
  date.setMonth(monthNumber - 1); return date.toLocaleString('en-US', { month: 'short' });
}console.log(getMonthName(1)); // Jan
console.log(getMonthName(2)); // Feb
console.log(getMonthName(3)); // Mar
```

或者我们可以使用`narrow`只显示第一个字母:

```
function getMonthName(monthNumber) {
  const date = new Date();
  date.setMonth(monthNumber - 1); return date.toLocaleString('en-US', { month: 'narrow' });
}console.log(getMonthName(1)); // J
console.log(getMonthName(2)); // F
console.log(getMonthName(3)); // M
```

**注意:**使用`narrow`可能会导致语言中以相同字母开头的月份名称不明确，例如一月、六月和七月。

有关选项的更多信息，您可以设置为`toLocaleString()`，查看 MDN 文档中的[本页](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat)。

# 国际机场。DateTimeFormat 对象

使用`toLocaleString()`意味着每次您想要一个对语言敏感的字符串时，您都必须指定一个`locale`和`options`。要使用相同的设置来格式化多个日期，我们可以使用一个 [Intl 的对象。改为 DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat) 类。

例如:

```
function getTwoConsecutiveMonthNames(monthNumber) {
  const date1 = new Date();
  date1.setMonth(monthNumber - 1); const date2 = new Date();
  date2.setMonth(monthNumber); const formatter = new Intl.DateTimeFormat('en-US', { month: 'short' }); // Format both dates with the same locale and options
  const firstMonth = formatter.format(date1);
  const secondMonth = formatter.format(date2); return `${firstMonth} & ${secondMonth}`;
}console.log(getTwoConsecutiveMonthNames(1)); // Jan & Feb
console.log(getTwoConsecutiveMonthNames(2)); // Feb & Mar
console.log(getTwoConsecutiveMonthNames(3)); // Mar & Apr
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/e3a115)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。