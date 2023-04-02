# 如何修复 JavaScript 中的“无法读取未定义的属性“0”错误

> 原文：<https://javascript.plainenglish.io/javascript-cannot-read-property-0-of-undefined-22d41b4e6f12?source=collection_archive---------1----------------------->

## 了解 JavaScript 中的“无法读取未定义的属性“0”错误以及如何轻松修复它。

![](img/7340a7bf767d8960c2ddda1532712a8b.png)

当您尝试访问类似数组的变量的`0`索引时，出现“无法读取 undefined 的属性‘0’”错误，但该变量却是`undefined`。要解决这个问题，您可以在访问索引之前将变量初始化为正确数据类型的值。

![](img/dcec7e1fc2cdff3a7f1b22fdd10c55a6.png)

根据您的情况，您可以通过执行下列操作之一来解决该错误:

1.  为变量提供定义的回退值。
2.  确保变量已经初始化。
3.  如果访问嵌套数组的索引，检查外部数组是否都不是`undefined`。

我们将在本文中触及这三种解决方案。

# 1.提供定义的回退值

我们可以修复 JavaScript 中的“无法读取未定义的属性' 0 '”错误，方法是在特定索引处访问变量之前给变量一个回退值。当访问可能返回值为`undefined`的对象的数组属性时，这种解决方案是有益的。

我们可以用[零合并操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) ( `??`)提供一个回退值:

```
// 👇 Initialize to empty array if undefined
const books = library.books ?? [];const firstBook = books[0];console.log(library.books); // undefinedconsole.log(firstBook); // undefined// Initialize to empty string if undefined
const content = firstBook ?? '';console.log(content); // '' (empty string)
```

如果不是`null`或`undefined`，nullish 合并运算符(`??`)将返回其左侧的值。如果是，那么`??`返回它右边的值。

```
console.log(2 ?? 5); *// 2*
console.log(undefined ?? 5); *// 5*
```

我们可以用[逻辑或](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR) ( `||`)运算符来代替`??`:

```
console.log(2 || 5); // 2
console.log(undefined || 5); // 5
```

# 2.确保变量初始化

当您访问未初始化的变量的`0`索引时，将出现 JavaScript 中的“无法读取未定义的属性‘0’”错误。JavaScript 中未初始化的变量的`default`值为`undefined`。

```
let arr;console.log(arr); // undefined// ❌ Cannot read properties of undefined (reading '0')
console.log(arr[0]);const str;// ❌ Cannot read properties of undefined (reading '0')
console.log(str[0]);
```

在这种情况下修复错误很容易；只需将变量设置为一个值，例如，数组为空数组(`[]`)，字符串为空字符串(`''`)，等等。

```
let arr = [];console.log(arr); // []// ✅ No error
console.log(arr[0]); // undefinedconst str = '';// ✅ No error
console.log(str[0]); // undefined
```

# 3.检查`undefined`的外部阵列

访问嵌套数组中的`0`索引时，也会出现“无法读取 undefined 的属性‘0’”错误。

```
const arr = [[1, 2, 3]];// ❌ Cannot read properties of undefined (reading '0')
console.log(arr[1][0]);
```

这里的数组只包含一个元素，所以访问`1`索引会返回`undefined`。访问`undefined`上的`0`索引会导致错误。

可选的链接运算符是防止这种错误的简洁方法:

```
const arr = [[1, 2, 3]];// ✅ No error
console.log(arr?.[1]?.[0]); // undefined
```

对于 nullish 值(`undefined`或`null`),[可选链接操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) ( `?.`)返回`undefined`，而不是尝试访问属性并导致错误。

由于外部数组的`1`索引返回了`undefined`，可选的链接操作符将阻止属性访问。

如果值不是 nullish，那么`?.`操作符将执行属性访问:

```
const words = [['javascript']];console.log(words?.[0]?.[0]); // javascriptconsole.log(words?.[0]?.[0]?.[0]); // j
```

*最初发表于*[*codingbeautydev.com*](https://cbdev.link/12b4b2)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。