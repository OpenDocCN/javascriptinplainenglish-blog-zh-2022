# 如何在 JavaScript 中获取两个字符之间的子串

> 原文：<https://javascript.plainenglish.io/javascript-get-substring-between-two-characters-d9cf76e41fe4?source=collection_archive---------9----------------------->

## 学习在 JavaScript 中获取两个字符之间的子字符串的多种方法。

![](img/4053a64d307d7951c01ef8d23864398a.png)

# 1.String substring()、indexOf()和 lastIndexOf()方法

要在 JavaScript 中获取字符串中两个字符之间的子字符串，请对字符串调用`slice()`方法，将第一个字符第一次出现后的索引作为第一个参数，将第二个字符最后一次出现的索引作为第二个参数。例如:

```
function getSubstring(str, char1, char2) {
  return str.substring(
    str.indexOf(char1) + 1,
    str.lastIndexOf(char2)
  );
}const str1 = 'one:two;three';
const substr1 = getSubstring(str1, ':', ';');
console.log(substr1); // twoconst str2 = 'one?two!three';
const substr2 = getSubstring(str2, '?', '!');
console.log(substr2); // two
```

`String` `indexOf()`方法返回一个值在字符串中第一次出现的位置。另一方面，`lastIndexOf()`返回一个值在字符串中最后一次出现的位置。

`String` `substring()`方法返回开始和结束索引之间的字符串部分，分别由第一个和第二个参数指定。我们将`1`添加到`indexOf()`的结果中，因为我们不希望第一个字符包含在我们试图获取的子字符串中。但是我们不需要从`lastIndexOf()`的结果中减去`1`，因为`substring()`已经排除了指定结束索引处的字符。

如果字符串中不存在该值，`indexOf()`和`lastIndexOf()`都将返回`-1`。这意味着当字符串中不存在第一个字符时，从第二个字符开始到最后一个字符出现的所有字符串都将包含在字符串中。

```
const str1 = 'one:two;three';
const substr1 = getSubstring(str1, '-', ';');
console.log(substr1); // one:two
```

此外，当第二个字符不存在时，从第一个字符开始到第一次出现的所有字符串都将包含在该字符串中。

```
const str1 = 'one:two;three';
const substr1 = getSubstring(str1, ':', '-');
console.log(substr1); // one
```

根据我们的用例，这可能不是我们想要的。如果我们希望在两个字符都不存在的情况下返回一个空字符串(`''`)，我们需要明确检查这一点:

```
function getSubstring(str, char1, char2) {
  const char1Index = str.indexOf(char1);
  const char2Index = str.lastIndexOf(char2);
  if (char1Index === -1) return '';
  if (char2Index === -1) return '';
  return str.substring(char1Index, char2Index);
}const str1 = 'one:two;three';
const substr1 = getSubstring(str1, '-', ';');
console.log(substr1); // '' (empty string)const substr2 = getSubstring(str1, ':', '-');
console.log(substr2); // '' (empty string)
```

# 2.String split()，Array slice()和 Array join()方法

下面是另一种获取字符串中两个字符之间的子字符串的方法:

```
function getSubstring(str, char1, char2) {
  return str
    .split(char1)
    .slice(1)
    .join('')
    .split(char2)
    .slice(0, -1)
    .join('');
}const str1 = 'one:two;three';
const substr1 = getSubstring(str1, ':', ';');
console.log(substr1); // twoconst str2 = 'one?two!three';
const substr2 = getSubstring(str2, '?', '!');
console.log(substr2); // two
```

`String` `split()`方法使用指定的分隔符分割字符串。

```
const str1 = 'one:two;three';// [ 'one', 'two;three' ]
console.log(str1.split(':'));
```

`Array` `slice()`方法提取开始和结束索引之间的数组元素，分别由第一个和第二个参数指定。我们将`1`作为第一个参数传递，而没有指定第二个参数，所以`slice()`从索引`1`处的元素中提取到字符串的末尾。

```
// ['two;three'];
console.log([ 'one', 'two;three' ].slice(1));
```

我们对`slice()`的结果调用`Array` `join()`方法，将数组的元素连接成一个字符串。

```
const str1 = 'one:two;three';// two;three
console.log(['two;three'].join(''));
```

我们再次分割这个结果，这次是通过第二个字符。

```
// ['two', 'three'];
console.log('two;three'.split(';'));
```

我们在这个拆分产生的数组上调用`slice()`，传递`0`和`-1`作为参数，将除最后一个元素之外的所有数组元素复制到一个新数组中。

```
// [ 'two' ]
console.log(['two', 'three'].slice(0, -1));
```

最后，我们对这个结果调用`join()`来获得两个字符之间的字符串。

与第一种方法不同，这种方法通过返回一个空字符串来处理其中一个字符不在字符串中的情况。

```
function getSubstring(str, char1, char2) {
  return str
    .split(char1)
    .slice(1)
    .join('')
    .split(char2)
    .slice(0, -1)
    .join('');
}const str1 = 'one:two;three';
const substr1 = getSubstring(str1, '-', ';');
console.log(substr1); // '' (empty string)const substr2 = getSubstring(str1, ':', '-');
console.log(substr2); // '' (empty string)
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/5d82a5)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**