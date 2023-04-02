# 如何在 JavaScript 中从数组创建集合

> 原文：<https://javascript.plainenglish.io/javascript-create-set-from-array-199a14afeeaa?source=collection_archive---------23----------------------->

![](img/fee44b634c58045153a2ae69028fcbdd.png)

要在 JavaScript 中从数组创建一个`Set`，将数组传递给`Set()`构造函数。例如:

```
const arr = [1, 2, 3];
const set = new Set(arr);console.log(set); // Set(3) { 1, 2, 3 }console.log(set.has(2)); // trueset.delete(2);console.log(set); // Set(2) { 1, 3 }
```

一个`Set`对象只存储唯一的值，所以它不会包含任何重复的值。

```
const arr = [1, 1, 2, 3, 3, 4];
const set = new Set(arr);// Set(4) { 1, 2, 3, 4 }
console.log(set);
```

这对于在不改变数组的情况下从数组中删除重复元素非常有用，例如:

```
const arr = [1, 1, 2, 3, 3, 4];const distinct = Array.from(new Set(arr));// [1, 2, 3, 4]
console.log(distinct);
```

*更新于:*[*【codingbeautydev.com】*](https://codingbeautydev.com/blog/javascript-create-set-from-array/)

每周获取新的 web 开发技巧和教程

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)