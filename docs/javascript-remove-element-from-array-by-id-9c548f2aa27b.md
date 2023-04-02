# 如何在 JavaScript 中通过 ID 从数组中移除元素

> 原文：<https://javascript.plainenglish.io/javascript-remove-element-from-array-by-id-9c548f2aa27b?source=collection_archive---------1----------------------->

## 了解如何在 JavaScript 中轻松地从数组中移除具有指定 ID 的对象。

![](img/12a8f5a57e5feb7a061d87825e526e36.png)

有时，我们可能会处理一组具有唯一 id 的对象，这些 id 允许在其他对象中唯一地标识每个对象。

例如:

```
const arr = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Peter' },
  { id: 3, name: 'Kate' },
];
```

如果我们想从数组中移除一个具有特定 ID 的对象，该怎么办？在本文中，我们将学习多种方法。

# 1.数组 findIndex()和 splice()方法

要在 JavaScript 中通过 ID 从数组中移除元素，使用`findIndex()`方法在数组中查找 ID 为的对象的索引。然后在数组上调用`splice()`方法，传递这个索引和`1`作为参数，从数组中移除对象。例如:

```
function removeObjectWithId(arr, id) {
  const objWithIdIndex = arr.findIndex((obj) => obj.id === id);
  arr.splice(objWithIdIndex, 1); return arr;
}const arr = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Kate' },
  { id: 3, name: 'Peter' },
];removeObjectWithId(arr, 2);// [ { id: 1, name: 'John' }, { id: 3, name: 'Peter' } ]
console.log(arr);
```

`Array` `findIndex()`方法返回数组中通过回调函数指定测试的第一个元素的索引。

```
const arr = [9, 8, 7, 6, 5];const index = arr.findIndex((num) => num === 7);
console.log(index); // 2
```

我们指定了一个测试，只有当数组中的对象的 ID 等于指定的 ID 时，该对象才会通过测试。这使得`findIndex()`返回具有该 ID 的对象的索引。

`Array` `splice()`方法通过删除现有元素同时添加新的元素来改变数组的内容。

```
const arr1 = ['a', 'b', 'c'];// Removing elements
arr1.splice(1, 2);
console.log(arr1); // [ 'a' ]// Removing and adding new elements
const arr2 = ['a', 'b', 'c'];
arr2.splice(1, 2, 'd', 'e');
console.log(arr2); // [ 'a', 'd', 'e' ]
```

这个方法有三个参数:

1.  `start` -开始改变数组的索引。
2.  `deleteCount` -要从`start`中移除的元素数量
3.  `item1, item2, ...` -要添加到数组中的可变数量的元素，从`start`开始。

我们指定一个`1`的`deleteCount`和一个`start`的目标索引，让`splice()`只从数组中移除具有该索引的对象。我们没有指定更多的参数，所以数组中没有添加任何东西。

## 避免副作用

`Array` `splice()`方法对传递的数组进行变异。这给我们的`removeObjectWithId()`函数带来了一个副作用。为了避免修改传递的数组并创建一个纯函数，制作数组的副本并在副本上调用`splice()`,而不是原始的

```
function removeObjectWithId(arr, id) {
  // Making a copy with the Array from() method
  const arrCopy = Array.from(arr); const objWithIdIndex = arrCopy.findIndex((obj) => obj.id === id);
  arrCopy.splice(objWithIdIndex, 1);
  return arrCopy;
}const arr = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Kate' },
  { id: 3, name: 'Peter' },
];const newArr = removeObjectWithId(arr, 2);// [ { id: 1, name: 'John' }, { id: 3, name: 'Peter' } ]
console.log(newArr);// original not modified
/**
[
  { id: 1, name: 'John' },
  { id: 2, name: 'Kate' },
  { id: 3, name: 'Peter' }
]
 */
console.log(arr);
```

## 小费

不修改外部状态的函数(即纯函数)更容易预测，也更容易推理。这使得限制程序中副作用的数量成为一个好习惯。

# 2.数组 filter()方法

我们也可以用`filter()`方法通过 ID 从数组中移除一个元素。我们在数组上调用`filter()`,传递一个回调函数，为数组中除了具有指定 ID 的对象之外的每个元素返回`true`。

## 例子

```
function removeObjectWithId(arr, id) {
  return arr.filter((obj) => obj.id !== id);
}const arr = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Kate' },
  { id: 3, name: 'Peter' },
];const newArr = removeObjectWithId(arr, 2);// [ { id: 1, name: 'John' }, { id: 3, name: 'Peter' } ]
console.log(newArr);// original not modified
/**
[
  { id: 1, name: 'John' },
  { id: 2, name: 'Kate' },
  { id: 3, name: 'Peter' }
]
 */
console.log(arr);
```

`Array` `filter()`方法创建一个新数组，其中填充了通过回调函数指定的测试的元素。它不会修改原始数组。

## 例子

```
const arr = [1, 2, 3, 4];const filtered = arr.filter((num) => num > 2);
console.log(filtered); // [ 3, 4 ]
```

在我们的示例中，我们设置了一个测试，只有当数组中的对象的`id`属性不等于指定的 ID 时，该对象才会通过测试。这确保了具有指定 ID 的对象不包含在从`filter()`返回的新数组中。

*更新于:*[*codingbeautydev.com*](https://cbdev.link/ab2b78)

您可以在哪里找到我们:

🌐[网站](https://cbdev.link/b621b9) |🌟推特 |🌟[脸书](http://facebook.com/CodingBeautyDev)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。