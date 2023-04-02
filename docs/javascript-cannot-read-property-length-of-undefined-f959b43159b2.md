# JavaScript 中“无法读取未定义的属性‘长度’”错误的 4 个快速修复

> 原文：<https://javascript.plainenglish.io/javascript-cannot-read-property-length-of-undefined-f959b43159b2?source=collection_archive---------7----------------------->

## 多种方法轻松解决 JavaScript 中的“无法读取未定义的属性‘长度’”错误

![](img/dbc18e395b7514f699a4dfd4e468f7f1.png)

你在 JavaScript 中遇到过“无法读取未定义的属性‘长度’”错误吗？当您试图从值为`undefined`的变量访问`length`属性时，会出现此错误。

```
const arr = undefined;// TypeError: Cannot read properties of undefined (reading 'length')
const length = arr.length;console.log(length);
```

要修复“无法读取未定义的属性‘长度’”错误，在从变量访问`length`属性之前，对变量执行`undefined`检查。有多种方法可以做到这一点，我们将在本文中介绍其中的 4 种。

# 1.使用 if 语句

在访问`length`属性之前，我们可以使用`if`语句来检查变量是否为真:

```
const arr = undefined;let arrLength = undefined;// Check if "arr" is truthy
if (arr) {
  arrLength = arr.length;
}console.log(arrLength); // undefined const str = undefined;let strLength = undefined;// Check if "str" is truthy
if (str) {
  strLength = str.length;
}console.log(strLength); // undefined
```

# 2.使用可选链接

我们可以使用[可选链接操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) ( `?.`)返回`undefined`，如果变量为 null(`null`或`undefined`)，则阻止方法调用:

```
const arr = undefined;// Use optional chaining on "arr" variable
const arrLength = arr?.length;console.log(arrLength); // undefined const str = undefined;// Use optional chaining on "str" variable
const strLength = str?.length;console.log(strLength); // undefined
```

# 3.访问回退值的长度属性

我们可以使用 [nullish 合并操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) ( `??`)来提供一个回退值，以便从其访问`length`属性。

```
const arr = undefined;// Providing an empty array fallback
const arrLength = (arr ?? []).length;console.log(arrLength); // 0 const str = undefined;// Providing an empty string fallback
const strLength = (str ?? '').length;console.log(strLength); // 0
```

如果不是`null`或`undefined`，则 nullish 合并运算符(`??`)返回其左侧的值。如果是，那么`??`返回其右边的值。

```
console.log(2 ?? 5); // 2
console.log(undefined ?? 5); // 5
```

我们还可以使用[逻辑 OR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR) (||)操作符来提供一个回退值，从这个值可以访问`length`属性。

```
const arr = undefined;// Providing an empty array fallback
const arrLength = (arr || []).length;console.log(arrLength); // 0const str = undefined;// Providing an empty string fallback
const strLength = (str || '').length;console.log(strLength); // 0
```

与`??`操作符一样，`||`如果不是`null`或`undefined`，则返回其左侧的值。如果是，那么`||`返回它右边的值。

# 4.使用回退值而不是访问 length 属性

我们还可以组合可选的链接操作符(`?.`)和无效合并操作符(`??`)来提供一个回退值作为结果，而不是从`undefined`值访问`length`属性。

```
const arr = undefined;// Using "0" as a fallback value
const arrLength = arr?.length ?? 0;console.log(arrLength); // 0 const str = undefined;// Using "0" as a fallback value
const strLength = str?.length ?? 0;console.log(strLength); // 0
```

正如我们之前看到的，逻辑 OR 运算符(`||`)可以在以下情况下代替`??`运算符:

```
const arr = undefined;// Using "0" as a fallback value
const arrLength = arr?.length || 0;console.log(arrLength); // 0const str = undefined;// Using "0" as a fallback value
const strLength = str?.length || 0;console.log(strLength); // 0
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/2f5285)

# ES13 中 11 个惊人的新 JavaScript 特性

本指南将带您快速了解 ECMAScript 13 中添加的所有最新功能。这些强大的新特性将会用更短、更富于表现力的代码来更新您的 JavaScript。

![](img/75a56482761ab63cfc081ad691d70d61.png)

[报名](https://cbdev.link/900477)立即免费领取一份。