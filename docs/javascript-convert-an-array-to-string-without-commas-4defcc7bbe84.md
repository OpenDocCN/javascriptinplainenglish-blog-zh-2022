# 如何在 JavaScript 中将数组转换为不带逗号的字符串

> 原文：<https://javascript.plainenglish.io/javascript-convert-an-array-to-string-without-commas-4defcc7bbe84?source=collection_archive---------6----------------------->

## 了解如何在 JavaScript 中将数组快速转换为不带逗号的字符串。

![](img/f330c840afea03a4569ff10af31d5c74.png)

要在 JavaScript 中将数组转换为不带逗号的字符串，请调用数组上的`join()`方法，并传递一个空字符串(`''`)作为参数:

```
const arr = ['coffee', 'milk', 'tea'];const withoutCommas = arr.join('');
console.log(withoutCommas); // coffeemilktea
```

`Array` `join()`方法返回一个字符串，该字符串包含与指定分隔符连接的每个数组元素。如果没有分隔符作为参数传递，它将使用逗号连接数组元素:

```
const arr = ['coffee', 'milk', 'tea'];const str = arr.join();
console.log(str); // coffee,milk,tea
```

我们可以指定除空字符串之外的其他分隔符，如连字符和斜线:

```
const arr = ['coffee', 'milk', 'tea'];const withHypens = arr.join('-');
console.log(withHypens); // coffee-milk-teaconst withSlashes = arr.join('/');
console.log(withSlashes); // coffee/milk/teaconst withSpaces = arr.join(' ');
console.log(withSpaces); // coffee milk tea
```

分隔符也可以包含多个字符:

```
const arr = ['coffee', 'milk', 'tea'];const withAnd = arr.join(' and ');
console.log(withAnd); // coffee and milk and teaconst withOr = arr.join(' or ');
console.log(withOr); // coffee or milk or tea
```

如果数组中的某个元素是`undefined`、`null`或空数组(`[]`)，则在与分隔符连接之前，该元素将被转换为空字符串(`''`)。例如:

```
const arr = ['coffee', null, 'milk', []];const withComma = arr.join(',');
console.log(withComma); // coffee,,milk,const withHyphen = arr.join('-');
console.log(withHyphen); // coffee--milk-
```

*更新于:*[*codingbeautydev.com*](https://codingbeautydev.com/blog/javascript-convert-array-to-string-without-commas/)

每周获取新的网站开发技巧和教程。

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)