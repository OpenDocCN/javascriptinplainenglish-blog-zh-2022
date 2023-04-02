# 如何在 JavaScript 中获取字符串的最后一个字符

> 原文：<https://javascript.plainenglish.io/javascript-get-last-character-of-string-4a7ac4d52bea?source=collection_archive---------15----------------------->

## 学习在 JavaScript 中轻松获取字符串最后一个字符的不同方法。

![](img/61346db230f9f112c1760283cfe0c4cd.png)

在本文中，我们将探讨一些在 JavaScript 中轻松获取字符串最后一个字符的方法。

# 1.String charAt()方法

要获得字符串的最后一个字符，我们可以对字符串调用`charAt()`方法，将最后一个字符索引作为参数传递。例如，`str.charAt(str.length - 1)`返回包含字符串最后一个字符的新字符串。

```
const str = 'book';const lastCh = str.charAt(str.length - 1);
console.log(lastCh); // k
```

`String` `charAt()`方法获取一个索引并返回该索引处的字符串字符。

## 小费

在 JavaScript 中，数组使用从零开始的索引。这意味着第一个字符的索引为`0`，最后一个字符的索引为`str.length - 1`。

## 注意

如果我们将一个不存在于字符串中的索引传递给`charAt()`，它将返回一个空字符串(`''`):

```
const str = 'book';const lastCh = str.charAt(10);
console.log(lastCh); // ''
```

# 2.字符串括号符号

我们也可以使用括号符号(`[]`)来访问字符串的最后一个字符。就像使用`charAt()`方法一样，我们使用`str.length - 1`作为索引来访问最后一个字符。

```
const str = 'book';const lastCh = str[str.length - 1];
console.log(lastCh); // k
```

## 注意

与`charAt()`不同，使用括号符号访问字符串中不存在的索引处的字符将返回`undefined`:

```
const str = 'book';const lastCh = str[10];
console.log(lastCh); // undefined
```

# 3.字符串拆分()和数组弹出()

使用这个方法，我们在字符串上调用`split()`方法来获得一个字符数组，然后我们在这个数组上调用`pop()`来获得字符串的最后一个字符。

```
const str = 'book';const lastCh = str.split('').pop();
console.log(lastCh); // k
```

我们将一个空字符串(`''`)传递给`split()`方法，将该字符串拆分成一个包含所有字符的数组。

```
const str = 'book';console.log(str.split('')); // [ 'b', 'o', 'o', 'k' ]
```

Array `pop()`方法从数组中移除最后一个元素并返回该元素。我们在字符数组上调用它来获取最后一个字符。

*更新于:*[【codingbeautydev.com】T21](https://cbdev.link/bc4a12)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/c540b3073d35ba821d506504618c25a3.png)

在 这里免费获得一份 [**。**](https://codingbeautydev.com/crazy-js-book/)