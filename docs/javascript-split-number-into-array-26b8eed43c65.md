# 如何在 JavaScript 中将一个数字拆分成一个数组

> 原文：<https://javascript.plainenglish.io/javascript-split-number-into-array-26b8eed43c65?source=collection_archive---------11----------------------->

![](img/47725897cd2740d6e1298f774cc19199.png)

# 1.Array.from()方法

要在 JavaScript 中将一个数字拆分成一个数组，调用`Array.from()`方法，将转换成字符串的数字作为第一个参数传递，将`Number`构造函数作为第二个参数传递，即`Array.from(String(num), Number)`。例如:

```
function splitIntoArray(num) {
  return Array.from(String(num), Number);
}const arr1 = splitIntoArray(1234);
console.log(arr1); // [ 1, 2, 3, 4 ]const arr2 = splitIntoArray(4901);
console.log(arr2); // [ 4, 9, 0, 1 ]
```

静态的`Array` `from()`方法从一个类似数组的对象创建一个新数组，比如`String`或`Set`。

```
// [ '1', '2', '3', '4' ]
console.log(Array.from('1234'));
```

我们传递给`from()`的第二个参数是在数组的每个元素上调用的 map 函数。我们传递了`Number`构造函数，这样数组中的每一项都将被转换成一个数字。

我们可以用`Array` `map()`实例方法更明确地做到这一点:

```
const num = 1234;// ['1', '2', '3', '4'];
const arrOfStrs = Array.from(String(num));const arrOfNums = arrOfStrs.map((str) => Number(str));console.log(arrOfNums); // [ 1, 2, 3, 4 ]
```

# 2.String split()方法

我们也可以用`String` `split()`方法将一个数拆分成一个数组。为此:

1.  将数字转换为字符串。
2.  对字符串调用`split()`方法，将其转换为字符串化数字的数组。
3.  在这个数组上调用`map()`方法将每个字符串转换成一个数字。

```
function splitIntoArray(num) {
  return String(num).split('').map(Number);
}const arr1 = splitIntoArray(1234);
console.log(arr1); // [ 1, 2, 3, 4 ]const arr2 = splitIntoArray(4901);
console.log(arr2); // [ 4, 9, 0, 1 ]
```

`String` `split()`方法根据指定的分隔符将一个字符串分成一个子字符串数组。我们指定一个空字符串(`''`)作为分隔符，将字符串分割成一个包含所有字符的数组。

```
// ['1', '2', '3', '4'];
console.log('1234'.split(''));
```

我们在这个字符串数组上调用`map()`，传递`Number`构造函数将每个元素转换成一个数字，并创建一个新的数字数组。

```
// [ 1, 2, 3, 4 ]
console.log(['1', '2', '3', '4'].map(Number));
```

## 小费

这个:

```
// [1, 2, 3, 4]
console.log(['1', '2', '3', '4'].map(Number));
```

产生与此相同的结果:

```
// [ 1, 2, 3, 4 ]
console.log(['1', '2', '3', '4']
  .map((str) => Number(str)));
```

尽管您可能更喜欢第二种方式，这样您就可以确切地看到您传递给`Number`的回调参数。

【codingbeautydev.com】更新于:[](https://cbdev.link/3e84d9)

# *JavaScript 做的每一件疯狂的事情*

*一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。*

*![](img/143ee152ba78025ea8643ba5b9726a20.png)*

*[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。*