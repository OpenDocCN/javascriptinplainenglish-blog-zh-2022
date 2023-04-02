# 检查 JavaScript 中的字符串是否包含特殊字符

> 原文：<https://javascript.plainenglish.io/javascript-check-if-string-contains-special-characters-8e9e1f1e74bd?source=collection_archive---------4----------------------->

## 了解在 JavaScript 中轻松检查字符串是否包含特殊字符的不同方法。

![](img/9ebe9bb1f362095d8558d51affc1795f.png)

在本文中，我们将研究一些方法来轻松检查 JavaScript 中的字符串是否包含特殊字符。

# 1.RegExp 测试()方法

为了检查 JavaScript 中的字符串是否包含特殊字符，我们可以根据匹配任何特殊字符的正则表达式来测试字符串。为此我们可以使用`RegExp` `test()`的方法:

```
function containsSpecialChars(str) {
  const specialChars =
    /[`!@#$%^&*()_+\-=\[\]{};':"\\|,.<>\/?~]/;
  return specialChars.test(str);
}console.log(containsSpecialChars('book_club')); // true
console.log(containsSpecialChars('milk')); // false
console.log(containsSpecialChars('2 + 3 = 5')); // true// Usage in if statement
if (containsSpecialChars('book_club')) {
  console.log('Special characters found.');
} else {
  console.log('No special characters found.');
}
```

`test()`方法使用正则表达式在字符串中搜索匹配项。如果找到匹配，它返回`true`，否则，它返回`false`。

# 2.Array some()方法

检查字符串是否包含特殊字符的另一种方法是使用`Array` `some()`方法:

```
function containsSpecialChars(str) {
  const specialChars =
    '[`!@#$%^&*()_+-=[]{};\':"\\|,.<>/?~]/';
  return specialChars
    .split('')
    .some((specialChar) => str.includes(specialChar));
}console.log(containsSpecialChars('book_club')); // true
console.log(containsSpecialChars('milk')); // false
console.log(containsSpecialChars('2 + 3 = 5')); // true// Usage in if statement
if (containsSpecialChars('book_club')) {
  console.log('Special characters found.');
} else {
  console.log('No special characters found.');
}
```

首先，我们创建一个包含所有特殊字符的字符串。注意，我们必须使用反斜杠转义(`\`)来将单引号(`'`)包含在单引号字符串中。

然后我们调用`String` `split()`方法，传递一个空字符串(`''`)作为参数，将字符串拆分成一个包含所有特殊字符的数组。

```
/** [
  '[', '`', '!', '@',  '#', '$', '%',
  '^', '&', '*', '(',  ')', '_', '+',
  '-', '=', '[', ']',  '{', '}', ';',
  "'", ':', '"', '\\', '|', ',', '.',
  '<', '>', '/', '?',  '~', ']', '/'
] */
const specialChars =
  '[`!@#$%^&*()_+-=[]{};\':"\\|,.<>/?~]/';
console.log(specialChars.split(''));
```

方法测试数组中的任何元素是否满足测试回调函数中指定的条件。如果数组中至少有一个元素通过测试，它将返回`true`。否则，返回`false`。

在我们的示例中，特殊字符数组中的元素只有在字符串包含该元素时才通过测试。因此，如果字符串包含至少一个特殊字符，`some()`将返回`true`。

*更新于:*[【codingbeautydev.com】T21](https://cbdev.link/081b1a)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。