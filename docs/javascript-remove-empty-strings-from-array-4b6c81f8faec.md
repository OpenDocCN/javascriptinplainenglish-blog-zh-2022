# 如何在 JavaScript 中移除数组中的空字符串

> 原文：<https://javascript.plainenglish.io/javascript-remove-empty-strings-from-array-4b6c81f8faec?source=collection_archive---------6----------------------->

![](img/2c9581e07738ca95ea6363399a973f73.png)

要在 JavaScript 中从数组中移除空字符串，请在数组上调用`filter()`方法，传递一个回调函数，该函数为数组中不是空字符串的每个元素返回`true`。`filter()`方法将返回一个新的数组，不包括空字符串。

例如:

```
const arr = ['c', '', 'o', '', '', 'd', '', 'e'];const noEmptyStrings = arr.filter((str) => str !== '');console.log(noEmptyStrings); // [ 'c', 'o', 'd', 'e' ]
```

`[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)`[filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)`方法创建一个新的数组，其中填充了通过回调函数指定的测试的元素。它不会修改原始数组。

```
const arr = [1, 2, 3, 4];const filtered = arr.filter((num) => num > 2);
console.log(filtered); // [ 3, 4 ]
```

在我们的例子中，数组中的每个元素只有在不是空字符串的情况下才会通过测试(`''`)。因此结果数组中不包含空字符串。

# 用循环从数组中删除空字符串

这里有一种在 JavaScript 中从数组中移除空字符串的替代方法。

```
const arr = ['c', '', 'o', '', '', 'd', '', 'e'];const noEmptyStrings = [];for (const item of arr) {
  if (item !== '') {
    noEmptyStrings.push(item);
  }
}console.log(noEmptyStrings); // [ 'c', 'o', 'd', 'e' ]
```

我们创建一个数组变量(`noEmptyStrings`)，它将存储原始数组中非空字符串的元素。然后我们使用一个`[for..of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)`循环来迭代数组。对于每个元素，我们使用`if`语句检查它是否为非空字符串。如果是，我们将它添加到数组变量中。在循环结束时，我们将得到一个不包含空字符串的数组。

两种方法都可以，它们之间的主要区别在于第一种方法是声明性的和函数性的。这是一个简短的[一行程序](https://codingbeautydev.com/blog/javascript-one-liners/),它使用了一个纯粹的函数，并专注于结果。但是第二种方法是必要的，因为它强调了获得结果所采取的步骤。

*最初发表于*[*codingbeautydev.com*](https://cbdev.link/d0a40e)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****