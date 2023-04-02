# JavaScript 中 7 个鲜为人知的数组方法

> 原文：<https://javascript.plainenglish.io/little-known-array-methods-javascript-3aee9ae8758a?source=collection_archive---------1----------------------->

![](img/34ed8a7a25e40d8df6de49e876929e4f.png)

在 JavaScript 中使用数组时，您可能会发现自己只使用了流行的方法，如`map()`、`filter()`、`find()`、`push()`和`sort()`。这是可以理解的，因为这些非常有用的方法对于许多用例来说已经足够了。

但是 JavaScript 有 30 多种数组方法，其中一些不太为人所知，许多 JavaScript 开发人员很少使用，尽管它们非常强大，能够解决现实世界中的问题。

因此，在本文中，我们将研究 7 种鲜为人知的 JavaScript 数组方法。我们将了解它们是如何工作的，并看看我们如何在实践中使用它们。

# 1.copyWithin()

[copyWithin()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin) 方法将数组的一部分复制到同一个数组中的另一个位置并返回，不增加其长度。

例如:

```
const array = [1, 2, 3, 4, 5];const result = array.copyWithin(3, 1, 3);console.log(result); // [1, 2, 3, 2, 3]
```

如果您不熟悉这种方法，您可能会发现这里的结果令人困惑。为了理解`copyWithin()`的工作原理，让我们来看看它的参数:

1.  `target`:数组中指定部分复制到的位置。
2.  `start`:将被复制的零件的起始索引。
3.  `end`:将被复制的零件的结束索引。

因此，通过分别传递`3`、`1`和`3`，我们告诉`copyWithin()`获取索引`1`和`3`之间的数组元素，并将它们复制到数组的另一部分，从索引`3`开始。这意味着`copyWithin()`从元素`4`所在的地方开始复制元素`1`和`2`，替换`4`和`5`。

让我们看另一个例子:

```
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];// "end" not specified so last array index used
const result = array.copyWithin(0, 5);// [6, 7, 8, 9, 10, 6, 7, 8, 9, 10]
console.log(result);
```

这里我们告诉`copyWithin()`开始将数字`6`、`7`、`8`、`9`和`10`复制到`1`所在的位置，替换任何连续的元素，直到`10`(最后一个元素)被复制。

如前所述，`copyWithin()`不会增加数组的长度，但会在到达数组末尾时停止复制。

```
const array = [1, 2, 3, 4, 5];// Copy numbers 2, 3, 4, and 5
const result = array.copyWithin(3, 1, 6);console.log(result); // [1, 2, 3, 2, 3]
```

# 2.在()

这个方法是新的 [ES13 JavaScript 特性](https://codingbeautydev.com/es13-javascript-features/)之一，它提供了一种更简洁的方式来从数组的末尾访问元素。

不要像这样写代码:

```
const arr = ['a', 'b', 'c', 'd'];// 1st element from the end
console.log(arr[arr.length - 1]); // d// 2nd element from the end
console.log(arr[arr.length - 2]); // c
```

有了 [at()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/at) ，我们可以更简洁、更有表现力地做到这一点，就像这样:

```
const arr = ['a', 'b', 'c', 'd'];// 1st element from the end
console.log(arr.at(-1)); // d// 2nd element from the end
console.log(arr.at(-2)); // c
```

我们简单地传递一个负值`-N`来访问数组末尾的第`N`个元素。

# 3.reduceRight()

[reduceRight()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight) 方法的工作方式类似于更流行的 [reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) 方法，不同之处在于回调函数从右到左应用于数组的每个值，而不是从左到右。

```
const letters = ['b', 'e', 'a', 'u', 't', 'y'];const word = letters.reduce((word, letter) => word + letter, '');console.log(word); // beauty const wordReversed = letters.reduceRight((word, letter) => word + letter, '');console.log(wordReversed); // ytuaeb
```

`reduceRight()`从右到左对数组的每个元素重复执行传递的回调函数。我们在这里传递的回调只是将当前元素和累加器字符串连接起来，最终得到反转的单词。

当你希望一个列表从左到右表达，但从右到左计算时，`reduceRight()`会有所帮助。这里有一个例子:

```
const thresholds = [
  { color: 'blue', threshold: 0.7 },
  { color: 'orange', threshold: 0.5 },
  { color: 'red', threshold: 0.2 },
];const value = 0.9;const threshold = thresholds.reduceRight((color, threshold) =>
  threshold.threshold > value ? threshold.color : color
);console.log(threshold.color); // red
```

# 4.findLast()

在 [ES13](https://codingbeautydev.com/es13-javascript-features/) 中，JavaScript 的另一个新特性是 [findLast()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast) 方法，用于从最后一个元素开始搜索数组中的一个元素。

在我们知道从最后一个元素中查找可能比使用`find()`方法获得更好的性能的情况下，我们可以使用它。

例如，这里我们试图获取数组中属性为`value`等于`'y'`的项目。带`find()`:

```
const letters = [
  { value: 'v' },
  { value: 'w' },
  { value: 'x' },
  { value: 'y' },
  { value: 'z' },
];const found = letters.find((item) => item.value === 'y');console.log(found); // { value: 'y' }
```

这是可行的，但是由于目标对象更靠近数组的尾部，如果我们使用`findLast()`方法从末尾搜索数组，我们可能会使程序运行得更快:

```
const letters = [
  { value: 'v' },
  { value: 'w' },
  { value: 'x' },
  { value: 'y' },
  { value: 'z' },
];const found = letters.findLast((item) => item.value === 'y');console.log(found); // { value: 'y' }
```

`findLast()`的另一个用例是当我们必须从数组的末尾开始搜索以获得正确的元素时。

例如，如果我们想找到一个数字列表中的最后一个偶数，`find()`会产生一个完全错误的结果:

```
const nums = [7, 14, 3, 8, 10, 9];// gives 14, instead of 10
const lastEven = nums.find((value) => value % 2 === 0);console.log(lastEven); // 14
```

但是`findLast()`会从头开始搜索，给我们正确的项目:

```
const nums = [7, 14, 3, 8, 10, 9];const lastEven = nums.findLast((num) => num % 2 === 0);console.log(lastEven); // 10
```

# 5.findLastIndex()

[findLastIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex) 的工作方式类似于`findLast()`，但是它返回的是找到的元素的索引，而不是元素本身。

在下面的例子中，我们使用`findLastIndex()`找到数组中最后一个颜色为`red`的汽车对象的索引，并删除它。

```
const carQueue = [
  { color: 'yellow' },
  { color: 'red' },
  { color: 'green' },
  { color: 'red' },
  { color: 'blue' },
];const lastRedIndex = carQueue.findLastIndex((car) => car.color === 'red');// Remove car object with splice()
carQueue.splice(lastRedIndex, 1);/**
[
  { color: 'yellow' },
  { color: 'red' },
  { color: 'green' },
  { color: 'blue' }
]
 */
console.log(carQueue);
```

# 6.lastIndexOf()

方法的作用是:返回一个数组中可以找到的最后一个元素的索引。

```
const colors = ['a', 'e', 'a', 'f', 'a', 'b'];const index = colors.lastIndexOf('a');console.log(index); // 4
```

我们可以将第二个参数传递给`lastIndexOf()`来指定数组中的一个索引，在这个索引之后它应该停止搜索字符串:

```
const colors = ['a', 'e', 'a', 'f', 'a', 'b'];// Get last index of 'a' before index 3
const index1 = colors.lastIndexOf('a', 3);console.log(index1); // 2const index2 = colors.lastIndexOf('a', 0);console.log(index2); // 0const index3 = colors.lastIndexOf('f', 2);console.log(index3); // -1
```

# 7.平面地图()

[flatMap()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap) 方法使用给定的回调函数转换数组，然后将转换后的结果展平一级。

```
const arr = [1, 2, 3, 4];const withDoubles = arr.flatMap((num) => [num, num * 2]); console.log(withDoubles); // [1, 2, 2, 4, 3, 6, 4, 8]
```

在数组上调用`flatMap()`与调用 [map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 后跟深度为 1 的 [flat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat) 的作用相同，但这比分别调用这两个方法更有效。

```
const arr = [1, 2, 3, 4];// flat() uses a depth of 1 by default
const withDoubles = arr.map((num) => [num, num * 2]).flat();console.log(withDoubles); // [1, 2, 2, 4, 3, 6, 4, 8]
```

# 结论

所以我们看了 JavaScript 中一些不太流行的数组方法。许多开发人员可能不知道它们，但毫无疑问它们是有用的。你可能很快就会需要其中一个。

*原载于*[【codingbeautydev.com】T21](https://cbdev.link/d47e37)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[报名](https://cbdev.link/d3c4eb)立即免费领取一份。