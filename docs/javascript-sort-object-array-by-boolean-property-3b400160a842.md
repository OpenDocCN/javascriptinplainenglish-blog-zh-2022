# 如何在 JavaScript 中通过布尔属性对对象数组进行排序

> 原文：<https://javascript.plainenglish.io/javascript-sort-object-array-by-boolean-property-3b400160a842?source=collection_archive---------5----------------------->

![](img/11bf97deea4a6a6ff23df37790cb68e5.png)

要通过 JavaScript 中的布尔属性对对象数组进行排序，请使用回调作为参数调用数组上的`sort()`方法。在函数中，使用 boolean 属性返回计算结果为正数、负数或零的表达式。这将按布尔属性对数组进行就地排序，即:

```
const trueFirst = users.sort((a, b) => b.boolProp - a.boolProp);

const falseFirst = users.sort((a, b) => a.boolProp - b.boolProp);
```

例如:

```
const users = [
  { name: 'Kate', premium: false },
  { name: 'Bob', premium: true },
  { name: 'Jeff', premium: false },
  { name: 'Samantha', premium: true },
];

const premiumFirst = users.sort((a, b) => b.premium - a.premium);

/*
  [
    { name: 'Bob', premium: true },
    { name: 'Samantha', premium: true },
    { name: 'Kate', premium: false },
    { name: 'Jeff', premium: false }
  ]
*/
console.log(premiumFirst);

const nonPremiumFirst = users.sort((a, b) => a.premium - b.premium);

/*
  [
    { name: 'Kate', premium: false },
    { name: 'Jeff', premium: false },
    { name: 'Bob', premium: true },
    { name: 'Samantha', premium: true }
  ]
*/
console.log(nonPremiumFirst);
```

`[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)`[sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)`方法将回调函数作为参数。它使用从该回调返回的值来确定对值进行排序的顺序。对于数组中的每个项目对，`a`和`b`:

如果返回值为负，则在排序后的数组中，`a`被放置在`b`之前。

如果值为正，`b`放在`a`之前。

如果值为`0`，则`a`和`b`的顺序不变。

```
const arr = [5, 3, 8, 1, 7];

// Sort in ascending order
arr.sort((a, b) => a - b);

console.log(arr); // [ 1, 3, 5, 7, 8 ]

// Sort in descending order
const desc = arr.sort((a, b) => b - a);

console.log(desc); // [ 8, 7, 5, 3, 1 ]
```

因为我们对布尔值使用了减法运算符(`-`)，所以在减法发生之前，它们被强制转换为数字。真值被强制为`1`，假值被强制为`0`。

```
console.log(true + true); // 2

console.log(true + false); // 1

console.log(false + false); // 0
```

在了解了`sort()`方法和布尔强制的工作原理之后，就很容易理解将布尔属性值为`true`的对象放置在布尔属性值为`false`的对象之上的排序方式，反之亦然。

# 按布尔属性对对象数组进行无突变排序

`sort()`方法就地对数组进行排序，这意味着它被修改了。为了防止这种情况，我们可以使用 [spread 语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) ( `...`)为排序创建数组的浅层副本:

```
const users = [
  { name: 'Kate', premium: false },
  { name: 'Bob', premium: true },
  { name: 'Jeff', premium: false },
  { name: 'Samantha', premium: true },
];

// 👇 Clone array with spread syntax
const premiumFirst = [...users].sort((a, b) => b.premium - a.premium);

/*
  [
    { name: 'Bob', premium: true },
    { name: 'Samantha', premium: true },
    { name: 'Kate', premium: false },
    { name: 'Jeff', premium: false }
  ]
*/
console.log(premiumFirst);

/*
  Original not modified:
  [
    { name: 'Kate', premium: false },
    { name: 'Bob', premium: true },
    { name: 'Jeff', premium: false },
    { name: 'Samantha', premium: true }
  ]
*/
console.log(users);
```

通过避免突变，我们可以使代码更具可读性、可预测性和模块化。

*最初发表于*【codingbeautydev.com】

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*