# 在 JavaScript 中交换 2 个数组元素的 3 种简单方法

> 原文：<https://javascript.plainenglish.io/javascript-swap-array-elements-4b176eb607c8?source=collection_archive---------10----------------------->

![](img/2a143c3f2822fd5a60c03b75b3872eb0.png)

在本文中，我们将学习在 JavaScript 中轻松交换两个数组元素的值的多种方法。

# 1.临时变量

在 JavaScript 中交换两个数组元素:

1.  创建一个临时变量来存储第一个元素的值。
2.  将第一个元素设置为第二个元素的值。
3.  将第二个元素设置为临时变量中的值。

例如:

```
function swapElements(arr, i1, i2) {
  // Step 1
  let temp = arr[i1]; // Step 2
  arr[i1] = arr[i2]; // Step 3
  arr[i2] = temp;
}const arr = [1, 2, 3, 4];swapElements(arr, 0, 3);console.log(arr); // [ 4, 2, 3, 1 ]
```

# 2.数组析构赋值

要使用此方法交换两个数组元素:

1.  创建一个新数组，以特定顺序包含这两个元素。
2.  使用 JavaScript 数组析构语法将数组中的值解包到一个新数组中，该数组以相反的顺序包含这两个元素。

使用这种方法，我们可以创建一个简洁的[一行程序](https://codingbeautydev.com/blog/javascript-one-liners/)来完成这项工作。

```
function swapElements(arr, i1, i2) {
  [arr[i1], arr[i2]] = [arr[i2], arr[i1]];
}const arr = [1, 2, 3, 4];swapElements(arr, 0, 3);console.log(arr); // [ 4, 2, 3, 1 ]
```

# 3.数组拼接()方法

交换两个数组元素的另一种方法是使用`splice()`方法，如下所示:

```
function swapElements(arr, i1, i2) {
  arr[i1] = arr.splice(i2, 1, arr[i1])[0];
}const arr = [1, 2, 3, 4];swapElements(arr, 0, 3);console.log(arr); // [ 4, 2, 3, 1 ]
```

`Array` `splice()`方法通过移除现有元素来改变数组的内容，同时可能在它们的位置添加新元素。

```
const arr1 = ['a', 'b', 'c'];// Removing elements
arr1.splice(1, 2);
console.log(arr1); // [ 'a' ]// Removing and adding new elements
const arr2 = ['a', 'b', 'c'];
arr2.splice(1, 2, 'd', 'e');
console.log(arr2); // [ 'a', 'd', 'e' ]
```

为了交换数组元素，我们为`splice()`的三个参数指定了某些参数:

1.  `start`:指定数组改变的起始索引。我们使用第二个元素的索引作为参数的自变量。
2.  `deleteCount`:这是一个数字，表示要从`start`中删除的元素数量。我们传递的`1`意味着只有在`start`索引处的元素(第二个要交换的元素)将被移除。
3.  `item1`，...，`itemN`:这些是要添加到数组中的可变数量的参数。我们只为此传递一个值——要交换的第一个元素。

所以我们传递给`splice()`的三个参数用第二个元素替换了第一个元素。

为了完成交换，我们利用了`splice()`返回包含移除元素的数组这一事实。

```
const arr2 = ['a', 'b', 'c'];const removed = arr2.splice(1, 2, 'd', 'e');console.log(removed); // [ 'b', 'c' ]
console.log(arr2); // [ 'a', 'd', 'e' ]
```

因此，对于我们的场景，要交换的第二个元素将在这个数组中，所以我们从数组中访问它，并将其值赋给第一个元素。

*最初发表于:*[*codingbeautydev.com*](https://cbdev.link/11e718)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。