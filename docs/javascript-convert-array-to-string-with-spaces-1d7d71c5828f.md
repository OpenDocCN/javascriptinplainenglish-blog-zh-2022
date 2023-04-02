# 如何在 JavaScript 中将数组转换成带空格的字符串

> 原文：<https://javascript.plainenglish.io/javascript-convert-array-to-string-with-spaces-1d7d71c5828f?source=collection_archive---------3----------------------->

## 了解如何在 JavaScript 中轻松地将数组转换为带空格的字符串。

![](img/2aae19f4e138cd47bd937c91f583f746.png)

要在 JavaScript 中将一个数组转换成一个带空格的字符串，调用数组上的`join()`方法，将包含空格的字符串作为参数传递。例如:

```
const arr = ['coffee', 'milk', 'tea'];const withSpaces = arr.join(' ');
console.log(withSpaces); // coffee milk tea
```

`Array` `join()`方法返回一个字符串，该字符串包含用指定分隔符连接的每个数组元素。如果没有分隔符作为参数传递，它将使用逗号连接数组元素:

```
const arr = ['coffee', 'milk', 'tea'];const str = arr.join();
console.log(str); // coffee,milk,tea
```

我们可以指定除空格之外的其他分隔符，如连字符和斜线:

```
const arr = ['coffee', 'milk', 'tea'];const withHypens = arr.join('-');
console.log(withHypens); // coffee-milk-teaconst withSlashes = arr.join('/');
console.log(withSlashes); // coffee/milk/tea
```

一个分隔符也可以包含多个字符。这允许我们用单词或多个空格来分隔数组元素。例如:

```
const arr = ['coffee', 'milk', 'tea'];const withAnd = arr.join(' and ');
console.log(withAnd); // coffee and milk and teaconst withOr = arr.join(' or ');
console.log(withOr); // coffee or milk or teaconst with2Spaces = arr.join('  ');
console.log(with2Spaces); // coffee  milk  tea
```

**注意:**如果数组中的一个元素是`undefined`、`null`或者空数组(`[]`)，那么在用分隔符串联之前，它将被转换为空字符串(`''`)。例如:

```
const arr = ['coffee', null, 'milk', []];const withComma = arr.join(',');
console.log(withComma); // coffee,,milk,const withSpaces = arr.join(' ');
console.log(withSpaces); // coffee  milk
```

*更新于:*[*codingbeautydev.com*](https://codingbeautydev.com/blog/javascript-convert-array-to-string-with-spaces/)

每周获取新的 web 开发技巧和教程。

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)