# 如何在 JavaScript 中在字符串的字符之间添加空格

> 原文：<https://javascript.plainenglish.io/javascript-add-space-between-characters-7edd4df91005?source=collection_archive---------7----------------------->

## 了解如何在 JavaScript 中轻松地在字符串字符之间添加空格。

![](img/5d28c090d01d3e579044df8d71dfc7ab.png)

在本文中，我们将学习如何在 JavaScript 中轻松地在字符串字符之间包含空格。

# 1.字符串 split()和 Split join()方法

要在字符串的字符之间添加一个空格，调用字符串上的`split()`方法获得一个字符数组，然后调用数组上的`join()`方法用空格分隔符连接字符。

例如:

```
function addSpace(str) {
  return str.split('').join(' ');
}const str1 = 'coffee';
const str2 = 'banana';console.log(addSpace(str1)); // c o f f e e
console.log(addSpace(str2)); // b a n a n a
```

`String` `split()`方法使用指定的分隔符将一个字符串分割成子字符串数组。

```
const str1 = 'coffee,milk,tea';
const str2 = 'sun-moon-star';console.log(str1.split(',')); // [ 'coffee', 'milk', 'tea' ]
console.log(str2.split('-')); // [ 'sun', 'moon', 'star' ]
```

通过使用一个空字符串(`''`)作为分隔符，我们将所有的字符串字符分割成单独的数组元素。

```
const str1 = 'coffee';
const str2 = 'banana';// Passing an empty string ('') to the split method// [ 'c', 'o', 'f', 'f', 'e', 'e' ]
console.log(str1.split(''));// [ 'b', 'a', 'n', 'a', 'n', 'a' ]
console.log(str2.split(''));
```

`String` `join()`方法用分隔符将数组中的每个字符串组合起来。它返回一个包含串联数组元素的新字符串。

```
const arr = ['a', 'b', 'c', 'd'];console.log(arr.join(' ')); // a b c d
console.log(arr.join('-')); // a-b-c-d
console.log(arr.join('/')); // a/b/c/d
```

因此，将一个空格字符传递给`join()`会在结果连接中用一个空格分隔字符。

有些情况下，字符串中的某些字符之间已经包含空格。在这种情况下，我们的方法会在字符之间添加更多的空格。

```
function addSpace(str) {
  return str.split('').join(' ');
}// These strings have spaces between some characters
const str1 = 'co  ffee';
const str2 = 'bana  na';console.log(addSpace(str1)); // c o     f f e e
console.log(addSpace(str2)); // b a n a     n a
```

这是因为空格(`' '`)也是一个字符，就像一个字母，调用`split()`会使它成为数组中的一个独立元素，它将与额外的空格组合在一起。

```
// These strings have spaces between some characters
const str1 = 'co  ffee';
const str2 = 'bana  na';// The space characters are separate elements of the
// array from split()
/**
 * [
  'c', 'o', ' ',
  ' ', 'f', 'f',
  'e', 'e'
]
 */
console.log(str1.split(''));/**
 * [
  'b', 'a', 'n',
  'a', ' ', ' ',
  'n', 'a'
]
 */
console.log(str2.split(''));
```

如果我们想避免字符的多重间距，我们可以在`split()`和`join()`之间插入一个对`filter()`方法的调用。

```
function addSpace(str) {
  return str
    .split('')
    .filter((item) => item.trim())
    .join(' ');
}// The strings have spaces between some characters
const str1 = 'co  ffee';
const str2 = 'bana  na';console.log(addSpace(str1)); // c o f f e e
console.log(addSpace(str2)); // b a n a n a
```

`Array` `filter()`方法返回一个新数组，该数组只包含原始数组中的元素，传递给`filter()`的测试回调函数为这些元素返回一个真值。在空格(`' '`)上调用`trim()`会导致空字符串(`''`)，这在 JavaScript 中不是真值。所以空格被排除在从`filter()`返回的结果数组之外。

## 小费

在 JavaScript 中，只有六个 falsy 值:`false`、`null`、`undefined`、`0`、`' '`(空字符串)和`NaN`。其他所有的价值都是真实的。

# 2.for…of 循环

对于更强制性的方法，我们可以使用 JavaScript `for...of`循环在字符串的字符之间添加一个空格。

```
function addSpace(str) {
  // Create a variable to store the eventual result
  let result = ''; for (const char of str) {
    // On each iteration, add the character and a space
    // to the variable
    result += char + ' ';
  } // Remove the space from the last character
  return result.trimEnd();
}const str1 = 'coffee';
const str2 = 'banana';console.log(addSpace(str1)); // c o f f e e
console.log(addSpace(str2)); // b a n a n a
```

为了处理前面讨论的场景，其中字符串在一些字符之间有空格，在每次迭代的字符上调用`trim()`,并在将它和空格添加到累加结果之前添加一个`if`检查以确保它是真的:

```
function addSpace(str) {
  // Create a variable to store the eventual result
  let result = ''; for (const char of str) {
    // On each iteration, add the character and a space
    // to the variable // If the character is a space, trim it to an empty
    // string, then only add it if it is truthy
    if (char.trim()) {
      result += char + ' ';
    }
  } // Remove the space from the last character
  return result.trimEnd();
}const str1 = 'co  ffee';
const str2 = 'bana  na';console.log(addSpace(str1)); // c o f f e e
console.log(addSpace(str2)); // b a n a n a
```

*最初发表于:*[*【codingbeautydev.com】*](https://cbdev.link/34da79)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。