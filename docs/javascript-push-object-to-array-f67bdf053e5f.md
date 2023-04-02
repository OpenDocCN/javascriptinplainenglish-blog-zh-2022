# 如何在 JavaScript 中将对象推送到数组中

> 原文：<https://javascript.plainenglish.io/javascript-push-object-to-array-f67bdf053e5f?source=collection_archive---------1----------------------->

![](img/6b4ad05a55328c77ded535bbf292d4e3.png)

在 JavaScript 中将对象推送到数组中，以对象为参数调用数组上的`push()`方法，即`arr.push(obj)`。`push()`方法会将元素添加到数组的末尾。

例如:

```
const arr = [];

const obj = { name: 'Jeff' };

// 👇 Push object to array
arr.push(obj);

// [{ name: 'Jeff' } ]
console.log(arr);
```

`[push()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)`方法获取一个对象并将其添加到数组的末尾。

# 初始化期间将对象推送到数组

如果变量是在对象被压入之前新创建的(就像前面的例子一样)，您可以简单地将对象放在方括号(`[]`)之间，以便在变量初始化时将它包含在数组中:

```
const obj = { name: 'Jeff' };

// 👇 Push object to array with initialization
const arr = [obj];

console.log(arr);
```

# 将多个对象推入数组

`push()`方法实际上接受可变数量的参数。它们按照传递给`push()`的顺序被添加到数组的末尾。

例如:

```
const arr = [];

const obj1 = { name: 'Samantha' };
const obj2 = { name: 'Chris' };
const obj3 = { name: 'Mike' };

arr.push(obj1, obj2, obj3);

// [ { name: 'Samantha' }, { name: 'Chris' }, { name: 'Mike' } ]
console.log(arr);
```

# 将对象推送到数组中而不发生突变

`push()`方法将一个对象添加到数组**中的**位置，这意味着它被修改了。如果你不想这样，你可以使用[展开语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) ( `...`)创建一个原始数组的副本，然后调用`push()`:

```
const arr = [{ name: 'Jerry' }];

const newArr = [...arr];

newArr.push({ name: 'Mia' });

// [ { name: 'Jerry' }, { name: 'Mia' } ]
console.log(newArr);

// 👇 Original not modified
console.log(arr); // [ { name: 'Jerry' } ]
```

与我们之前所做的类似，我们可以在 spread 语法之后的方括号中包含对象，以便在初始化时将对象推送到数组的副本:

```
const arr = [{ name: 'Jerry' }];

// 👇 Push object to array without mutation
const newArr = [...arr, { name: 'Mia' }];

// [ { name: 'Jerry' }, { name: 'Mia' } ]
console.log(newArr);

// Original not modified
console.log(arr); // [ { name: 'Jerry' } ]
```

虽然不总是必要的，但是通过避免突变，我们可以使我们的代码更加可读、可预测和模块化。

*最初发表于*[*codingbeautydev.com*](https://cbdev.link/7c771f)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**注册**](https://cbdev.link/d3c4eb) 即可免费领取一份。