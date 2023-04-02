# 如何在 JavaScript 中不修改的情况下反转数组

> 原文：<https://javascript.plainenglish.io/javascript-reverse-array-without-modifying-dac063623490?source=collection_archive---------16----------------------->

![](img/58b3f751629c79c6583e4ea960b03483.png)

让我们看看一些在 JavaScript 中不改变原始数组的情况下反转数组顺序的方法。

# 1.切片()和反转()

要在不修改原始数组的情况下反转数组，我们可以用`slice()`方法克隆数组，用`reverse()`方法反转克隆。

例如:

```
const arr = [1, 2, 3];
const reversed = arr.slice().reverse();console.log(reversed); // [ 3, 2, 1 ]
console.log(arr); // [ 1, 2, 3 ]
```

`reverse()`方法就地反转一个数组，所以我们在数组上不带参数地调用`slice()`方法，返回它的一个副本。

# 2.展开运算符和反转()

在 ES6+中，我们还可以在调用`reverse()`之前，通过使用 spread 语法将其元素解包到一个新数组中来克隆数组:

```
const arr = [1, 2, 3];
const reversed = [...arr].reverse();console.log(reversed); // [ 3, 2, 1 ]
console.log(arr); // [ 1, 2, 3 ]
```

# 3.反向 for 循环

我们还可以通过创建一个 reverse `for`循环来反转一个数组而不修改它，并且在每次迭代中，将索引是循环计数器的当前值的数组元素添加到一个新数组中。新数组将包含循环结束时反转的所有元素。

```
const arr = [1, 2, 3];
const reversed = [];
for (let i = arr.length - 1; i >= 0; i--) {
  reversed.push(arr[i]);
}console.log(arr); // [ 1, 2, 3 ]
console.log(reversed); // [ 3, 2, 1]
```

*更新于:*[*codingbeautydev.com*](https://codingbeautydev.com/blog/javascript-reverse-array-without-modifying/)

每周获取新的 web 开发技巧和教程。

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)