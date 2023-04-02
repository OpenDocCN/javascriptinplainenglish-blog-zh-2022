# 如何在 JavaScript 中获取地图的第一个元素

> 原文：<https://javascript.plainenglish.io/javascript-map-get-first-element-83cb665af9b5?source=collection_archive---------6----------------------->

![](img/08dc5347f0eda88e5a5e66f6db97cc84.png)

在本文中，我们将探索一些在 JavaScript 中快速获取`Map`对象的第一个元素的方法。

# 1.对映射条目()调用 next()

要获得一个`Map`的第一个元素，我们可以调用`Map`上的`entries()`来获得一个可迭代对象，然后调用这个可迭代对象上的`next()`方法。例如:

```
const map = new Map([
  ['key1', 'value1'],
  ['key2', 'value2'],
  ['key3', 'value3'],
]);const firstElement = map.entries().next().value;console.log(firstElement); // [ 'key1', 'value1' ]
```

`Map` `entries()`方法为`Map`的所有元素返回一个键值对的 iterable。方法返回 iterable 序列中的下一个元素。因为这是我们第一次在 iterable 上调用它，所以它返回序列中的第一个元素。我们使用元素的`value`属性来获取表示`Map`的第一个元素的键值对。

# 2.数组. from()

我们还可以使用`Array.from()`方法来获取`Map`的第一个元素:

```
const map = new Map([
  ['key1', 'value1'],
  ['key2', 'value2'],
  ['key3', 'value3'],
]);const firstElement = Array.from(map)[0];
console.log(firstElement); // [ 'key1', 'value1' ]
```

## 注意

在有许多元素的`Map`上，这种方法比第一种方法慢得多，因为它从所有的`Map`元素中创建一个新的数组。我们在具有 100 万个元素的`Map`上对这两种方法进行了性能比较，这些是平均结果:

```
Iterable next(): 0.015ms
Array from() 251.093ms
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/ae61a5)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。