# 如何在 JavaScript 中获取一个字符串的最后两个字符

> 原文：<https://javascript.plainenglish.io/javascript-get-last-two-characters-of-string-67fc4863c5b5?source=collection_archive---------6----------------------->

![](img/7ff532258412c127bc9630e9f5b11be7.png)

要在 JavaScript 中获得一个字符串的最后两个字符，对该字符串调用`slice()`方法，将`-2`作为参数传递。例如，`str.slice(-2)`返回包含`str`最后两个字符的新字符串。

```
const str = 'Coding Beauty';const last2 = str.slice(-2);
console.log(last2); // ty
```

`String()` `slice()`方法返回开始和结束索引之间的字符串部分，分别由第一个和第二个参数指定。当只指定了起始索引时，它返回该起始索引之后的整个字符串部分。

当我们传递一个负数作为参数时，`slice()`从最后一个字符串开始向后计数，以找到等价的索引。因此将`-2`传递给`slice()`指定了`str.length - 2`的开始索引。

```
const str = 'Coding Beauty';const last2 = str.slice(-2);
console.log(last2); // tyconst last2Again = str.slice(str.length - 2);
console.log(last2Again); // ty
```

## 小费

如果我们试图获取比字符串包含的更多的字符，`slice()`返回整个字符串，而不是抛出一个错误。

```
const str = 'Coding Beauty';const last50 = str.slice(-50);
console.log(last50); // Coding Beauty
```

在这个例子中，我们试图通过将`-50`作为第一个参数传递来获取字符串的最后 50 个字符，但是字符串`'Coding Beauty'`只包含 13 个字符。因此，我们从`slice()`获得整个字符串。

## 注意

我们可以用`substring()`代替`slice()`来获得字符串的前两个字符:

```
const str = 'Coding Beauty';const last2 = str.substring(str.length - 2);
console.log(last2); // ty
```

但是，我们必须自己用`str.length - 2`手动计算起始索引，这使得代码可读性较差。这是因为与`slice()`不同，如果传递的是负数，`substring()`使用`0`作为起始索引。

```
const str = 'Coding Beauty';// -2 is negative, 0 used as start index
const notLast2 = str.substring(-2);console.log(notLast2); // Coding Beauty
```

*更新于:【codingbeautydev.com】[](https://cbdev.link/7a9203)*

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*