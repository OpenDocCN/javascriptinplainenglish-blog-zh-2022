# 如何用 JavaScript 找到数组中的奇数

> 原文：<https://javascript.plainenglish.io/javascript-find-odd-numbers-in-array-79ce3d82fcc1?source=collection_archive---------0----------------------->

![](img/948d34244f675fb79c7fa9fa51d44990.png)

在本文中，我们将研究使用 JavaScript 在数组中寻找奇数的不同方法。

# 1.数组 filter()方法

为了找到数组中的奇数，我们可以调用`Array` `filter()`方法，传递一个回调函数，当数字为奇数时返回`true`，否则返回`false`。

```
const numbers = [8, 19, 5, 6, 14, 9, 13];const odds = numbers.filter((num) => num % 2 === 1);
console.log(odds); // [19, 5 , 9, 13]
```

`filter()`方法创建一个新的数组，其中包含通过测试回调函数中指定的测试的所有元素。所以，`filter()`返回原始数组中所有奇数的数组。

# 2.数组 forEach()方法

寻找 JavaScript 数组中奇数的另一种方法是使用`Array` `forEach()`方法。我们在数组上调用`forEach()`，在回调中，我们只在结果数组中添加一个奇数元素。例如:

```
const numbers = [8, 19, 5, 6, 14, 9, 13];const odds = [];
numbers.forEach((num) => {
  if (num % 2 === 1) {
    odds.push(num);
  }
});console.log(odds); // [19, 5, 9, 13]
```

# 3.for…of 循环

我们可以使用`for...of`循环代替`forEach()`来遍历数组:

```
const numbers = [8, 19, 5, 6, 14, 9, 13];const odds = [];
for (const num of numbers) {
  if (num % 2 === 1) {
    odds.push(num);
  }
}
console.log(odds); // [19, 5, 9, 13]
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/7862c6)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。