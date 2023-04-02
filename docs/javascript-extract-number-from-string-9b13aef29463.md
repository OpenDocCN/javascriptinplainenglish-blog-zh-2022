# 如何用 JavaScript 从字符串中提取一个数字

> 原文：<https://javascript.plainenglish.io/javascript-extract-number-from-string-9b13aef29463?source=collection_archive---------8----------------------->

## 了解在 JavaScript 中从字符串中轻松提取数字的多种方法。

![](img/dcca33a680ed283af5c0bcd7410c1090.png)

# 1.字符串替换()方法

要在 JavaScript 中从字符串中提取一个数字，用正则表达式调用字符串上的`replace()`方法来替换原始字符串中的所有非数字字符。例如:

```
const str = 'The number 345 has three digits';const replaced = str.replace(/\D/g, '');
console.log(replaced); // 345
```

`String` `replace()`方法返回一个新的字符串，其中匹配的模式被替换。我们传递一个匹配所有非数字字符的正则表达式，这样我们就可以用一个空字符串(`''`)来替换它们，从而删除它们。

`\D`正则表达式元字符匹配字符串中的任何非数字字符。

`g`(全局)标志指定字符串中出现的每一个非数字字符都应该由正则表达式进行匹配。

如果我们没有传递全局标志，那么只有输入字符串中的第一个非数字字符会被匹配和替换:

```
const str = 'The number 345 has three digits';// No 'g' flag in regex
const replaced = str.replace(/\D/, '');console.log(replaced); // he number 345 has three digits
```

# 2.字符串匹配()方法

为了从字符串中提取一个数字，我们还可以在字符串上调用`match()`方法，传递一个匹配连续数字序列的正则表达式。例如:

```
const str = 'The number 345 has three digits';const matches = str.match(/\d+/);
const numStr = matches[0];console.log(numStr); // 345
```

`String` `match()`方法根据正则表达式匹配字符串并返回结果。在我们的例子中，匹配的数字是数组的第一项，所以我们用括号符号访问`0`属性来获取它。

`\d`元字符用于查找字符串中的数字。我们将`+`与`\d`相加，以找到一个连续的数字序列。

当试图分别提取字符串中的每个数字时，第二种方法更好，因为它将连续的数字序列视为单独的匹配。为了分别提取每个数字，我们需要添加`g`标志:

```
const str = 'The numbers 345 and 847 have three digits';const matches = str.match(/\d+/g);
console.log(matches); // [ '345', '847' ]
```

## 注意

当找不到数字时，`match()`方法将返回`null`:

```
const str = 'There are no numbers in this string';const matches = str.match(/\d+/g);
console.log(matches); // null
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/50bc41)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。