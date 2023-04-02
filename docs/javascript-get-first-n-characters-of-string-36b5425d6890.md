# 如何在 JavaScript 中获取字符串的前 N 个字符

> 原文：<https://javascript.plainenglish.io/javascript-get-first-n-characters-of-string-36b5425d6890?source=collection_archive---------4----------------------->

## 了解如何使用 JavaScript 轻松获取字符串的前几个字符。

![](img/fe1d17ed7755734336d1f9eb7f045321.png)

# 1.slice()方法

要在 JavaScript 中获取一个字符串的前`N`个字符，调用该字符串的`slice()`方法，将`0`作为第一个参数，将`N`作为第二个参数。例如，`str.slice(0, 2)`返回包含`str`前两个字符的新字符串。

```
const str = 'Coding Beauty';const first2 = str.slice(0, 2);
console.log(first2); // Coconst first6 = str.slice(0, 6);
console.log(first6); // Codingconst first8 = str.slice(0, 8);
console.log(first8); // Coding B
```

`String` `slice()`方法提取开始和结束索引之间的字符串部分，分别由第一个和第二个参数指定。索引`0`和`N`之间的子串是只包含第一个`N`字符串字符的子串。

## 注意

JavaScript 中的字符串是不可变的，并且`slice()`方法返回一个新的字符串，而不修改原来的字符串:

```
const str = 'Coding Beauty';const first2 = str.slice(0, 2);
console.log(first2); // Co// Original not modified
console.log(str); // Coding Beauty
```

# 2.substring()方法

为了获得一个字符串的第一个`N`字符，我们也可以在字符串上调用`substring()`方法，分别传递`0`和`N`作为第一个和第二个参数。例如，`str.substring(0, 3)`返回包含`str`前 3 个字符的新字符串。

```
const str = 'Coding Beauty';const first3 = str.substring(0, 3);
console.log(first3); // Codconst first5 = str.substring(0, 5);
console.log(first5); // Codinconst first11 = str.substring(0, 11);
console.log(first11); // Coding Beau
```

像`slice()`一样，`substring()`返回开始和结束索引之间的字符串部分，分别由第一个和第二个参数指定。

## 注意

`substring()`返回一个新的字符串而不修改原来的:

```
const str = 'Coding Beauty';const first3 = str.substring(0, 3);
console.log(first3); // Cod// Original not modified
console.log(str); // Coding Beauty
```

## 小费

对于我们的场景，`slice()`和`substring()`方法的工作方式类似，但情况并非总是如此。它们之间有一个区别:`substring()`如果第一个参数大于第二个参数，则交换它的参数，但是`slice()`返回一个空字符串(`''`):

```
const str = 'Coding Beauty';const substr1 = str.substring(2, 0);
const substr2 = str.slice(2, 0);// Equivalent to str.substring(0, 2)
console.log(substr1); // Coconsole.log(substr2); // '' (empty string)
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/7f845a)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。