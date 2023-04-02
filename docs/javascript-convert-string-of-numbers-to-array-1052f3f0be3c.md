# 如何在 JavaScript 中将一串数字转换成数组

> 原文：<https://javascript.plainenglish.io/javascript-convert-string-of-numbers-to-array-1052f3f0be3c?source=collection_archive---------11----------------------->

## 了解如何在 JavaScript 中将包含逗号分隔的数字列表的字符串轻松转换为数组

![](img/64d85177cdd2c23649dd070a50134e7e.png)

在本文中，我们将学习如何在 JavaScript 中轻松地将包含逗号分隔的数字列表的字符串转换为这些数字的数组。

# 字符串拆分()和数组映射()方法

要将一串数字转换成数组，调用字符串上的`split()`方法，传递一个逗号(`,`)作为参数，以获得数字的字符串表示的数组。然后使用`map()`方法将数组中的每个字符串转换成一个数字。例如:

```
const str = '1,2,3,4';const nums = str.split(',').map(Number);
console.log(nums); // [ 1, 2, 3, 4 ]
```

`String` `split()`方法使用指定的分隔符将一个字符串分成一个字符数组。我们传递一个逗号来将字符串化的数字分隔成结果数组中的独立元素。

```
console.log('1,2,3,4'.split(',')); // [ '1', '2', '3', '4' ]
```

`Array` `map()`方法根据对原始数组的每个元素调用回调函数的结果创建一个新数组。我们将`Number`构造函数传递给`map()`，因此将对数组中的每个字符串调用`Number()`来将其转换为数字。

我们可以像这样更明确地使用`map()`方法:

```
const str = '1,2,3,4';const nums = str.split(',').map((item) => Number(item));
console.log(nums); // [ 1, 2, 3, 4 ]
```

您可能更喜欢这种方法，因为它可以让您确切地看到传递给回调函数的参数。这可以防止回调函数根据传递的参数数量表现不同的情况下出现错误。

除了`Number`构造函数，我们还可以用`parseInt()`将字符串数组中的每一项转换成一个数字:

```
const str = '1,2,3,4';const nums = str.split(',').map((item) => parseInt(item, 10));
console.log(nums); // [ 1, 2, 3, 4 ]
```

`parseInt()`解析字符串并返回指定底数的整数。我们将`10`作为第二个参数传递，因此`parseInt()`使用基数 10 来解析字符串。

我们也可以使用一元运算符(`+`)来代替`parseInt()`或`Number()`。该运算符将非数值转换为数字。

```
const str = '1,2,3,4';const nums = str.split(',').map((item) => +item);
console.log(nums); // [ 1, 2, 3, 4 ]
```

*更新于:*【codingbeautydev.com】

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*