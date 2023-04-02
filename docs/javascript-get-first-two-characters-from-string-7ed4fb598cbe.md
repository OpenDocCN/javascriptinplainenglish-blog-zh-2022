# 如何在 JavaScript 中获取字符串的前两个字符

> 原文：<https://javascript.plainenglish.io/javascript-get-first-two-characters-from-string-7ed4fb598cbe?source=collection_archive---------1----------------------->

## 了解如何在 JavaScript 中轻松获取字符串的前两个字符。

![](img/d4ff8b1eaac77cda91f6d3fdbfbf967c.png)

# 1.slice()方法

要在 JavaScript 中获得一个字符串的前两个字符，调用该字符串的`slice()`方法，分别传递`0`和`2`作为第一个和第二个参数。例如，`str.slice(0, 2)`返回包含`str`前两个字符的新字符串。

```
const str = 'Coding Beauty';const firstTwoChars = str.slice(0, 2);
console.log(firstTwoChars); // Co
```

`slice()`方法提取开始和结束索引之间的字符串部分，分别由第一个和第二个参数指定。索引`0`和`2`之间的子串是只包含前两个字符串字符的子串。

## 注意

JavaScript 中的字符串是不可变的，并且`slice()`方法返回一个新的字符串，而不修改原来的字符串:

```
const str = 'Coding Beauty';const first2 = str.slice(0, 2);
console.log(first2); // Co// Original not modified
console.log(str); // Coding Beauty
```

# 2.substring()方法

或者，要获得一个字符串的前两个字符，我们可以在该字符串上调用`substring()`方法，将`0`和`2`分别作为第一个和第二个参数传递。例如，`str.substring(0, 2)`返回包含`str`前两个字符的新字符串。

```
const str = 'Coding Beauty';const firstTwoChars = str.substring(0, 2);
console.log(firstTwoChars); // Co
```

像`slice()`一样，`substring()`方法返回开始和结束索引之间的字符串部分，分别由第一个和第二个参数指定。

## 注意

`substring()`返回一个新字符串而不修改原来的:

```
const str = 'Coding Beauty';const first2 = str.substring(0, 2);
console.log(first2); // Co// Original not modified
console.log(str); // Coding Beauty
```

## 小费

对于我们的用例来说,`slice()`和`substring()`的工作方式类似，但并不总是这样。它们之间有一个区别:`substring()`如果第一个参数大于第二个参数，就交换它的参数，但是`slice()`返回一个空字符串(`''`)。

```
const str = 'Coding Beauty';const substr1 = str.substring(2, 0);
const substr2 = str.slice(2, 0);// Equivalent to str.substring(0, 2)
console.log(substr1); // Coconsole.log(substr2); // '' (empty string)
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/45811c)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。