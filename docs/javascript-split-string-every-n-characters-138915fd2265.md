# 如何在 JavaScript 中每隔 n 个字符拆分一个字符串

> 原文：<https://javascript.plainenglish.io/javascript-split-string-every-n-characters-138915fd2265?source=collection_archive---------4----------------------->

## 了解如何在 JavaScript 中轻松地将一个字符串分割成 N 个字符长的子字符串。

![](img/bdfed68deca34033ef3bc3377d7e9dd1.png)

要在 JavaScript 中每 N 个字符分割一个字符串，调用字符串上的`match()`方法，将这个正则表达式:`/.{1, N}g/`作为参数传递。`match()`方法将返回一个包含子字符串的数组，每个子字符串有 N 个字符。

例如:

```
const str = 'codingbeauty';const result = str.match(/.{1,4}/g) ?? [];console.log(result); // [ 'codi', 'ngbe', 'auty' ];
```

`String` `[match()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match)`方法将一个字符串与一个正则表达式进行匹配，并返回所有匹配的数组。

正斜杠`/ /`表示正则表达式的开始和结束。

`.`(点)元字符匹配字符串中的任何单个字符。

形式为`{min, max}`的大括号至少匹配其前面模式的`min`个字符，最多匹配其前面模式的`max`个字符。在我们的例子中，该模式是`.`字符，`min`是`1`，max 是`4`，这意味着`.{1, 4}`匹配字符串中的 1 到 4 个字符。

我们使用`g`(全局)标志来匹配字符串中模式的每一次出现。它让正则表达式一直将字符串分割成 N 个字符，直到它到达末尾。

如果没有`g`标志，将只匹配模式的第一个实例。

```
const str = 'codingbeauty';// "g" flag not specified
const result = str.match(/.{1,4}/) ?? [];// [ 'codi' ... ] (single-item array)
console.log(result);
```

关于正则表达式语法的全面指南，请查看 MDN 文档中的这个[备忘单](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet)。

如果字符串中没有匹配的正则表达式，`match()`返回`null`。这就是为什么我们在这种情况下使用[空合并操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing) ( `??`)返回一个空数组(`[]`)。

```
const str = '';const result = str.match(/.{1,4}/g) || [];console.log(result); // []
```

如果是`null`或`undefined`，则`??`运算符返回其左侧的值。否则，它将返回其右侧的值。

```
console.log(null ?? 5); // 5console.log(2 ?? 5); // 2console.log(undefined ?? 10); // 10console.log('' ?? 10); // '' (empty string)
```

如果字符串的长度不是 N 的倍数，数组中的最后一个元素将小于 N。

```
const str = 'codingbeautydev';const result = str.match(/.{1,4}/g) ?? [];// 👇 Last item is less than 4 characters long
console.log(result); // [ 'codi', 'ngbe', 'auty', 'dev' ];
```

# 用`for`循环每 N 个字符分割一个字符串

或者，我们可以使用一个`for`循环每 N 个字符分割一个字符串。

```
function splitString(str, N) {
  const arr = []; for (let i = 0; i < str.length; i += N) {
    arr.push(str.substring(i, i + N));
  } return arr;
}// [ 'codi', 'ngbe', 'auty' ]
console.log(splitString('codingbeauty', 4));// [ 'codi', 'ngbe', 'auty', 'dev' ]
console.log(splitString('codingbeautydev', 4));
```

我们的`splitString()`函数将字符串和每个子字符串的长度作为参数。

我们使用`for`循环以 n 为增量迭代字符串。在每次迭代中，我们调用`String` `[substring()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)`方法来获取字符串中索引`i`和索引`i + N` exclusive 之间的子字符串，并将子字符串添加到结果数组中。

# 用`reduce()`方法每 N 个字符分割一个字符串

每当你看到一个`for`循环被用来处理输入以获得输出，这是一个信号，表明代码可以被重构，使用一个或多个`Array`方法变得更具功能性和声明性。

看看这个每 N 个字符分割一个字符串的方法，这里我们使用了`[reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)`方法来创建一些漂亮的函数魔术:

```
const splitString = (str, N) =>
  [...str]
    .reduce(
      (substrings, ch) =>
        (substrings.at(-1)?.length ?? N) < N
          ? [...substrings.slice(0, -1), substrings.at(-1) + ch]
          : [...substrings, ch],
      []
    );// [ 'codi', 'ngbe', 'auty' ]
console.log(splitString('codingbeauty', 4));// [ 'codi', 'ngbe', 'auty', 'dev' ]
console.log(splitString('codingbeautydev', 4));
```

但是我不推荐这样做；就性能而言，它明显比以前的方法慢(30 倍以上)，并且可能更难理解。我把它包括进来是因为它是一个优雅的[一行程序](https://codingbeautydev.com/blog/javascript-one-liners/)解决方案。

*最初发表于*[*codingbeautydev.com*](https://cbdev.link/e162f3)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**注册**](https://cbdev.link/d3c4eb) 即可免费领取一份。