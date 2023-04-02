# JavaScript Array.slice()方法是什么？

> 原文：<https://javascript.plainenglish.io/javascript-array-slice-method-58526c52bd85?source=collection_archive---------7----------------------->

## slice()方法用于根据可选的开始和结束参数返回数组的浅表副本。下面是 slice()方法的工作原理。

![](img/6362e23a319d5da86d9b74e329d91845.png)

数组上的`slice`方法返回数组一部分的浅表副本。它需要两个数字，一个`start`和一个`end`。每个数组都有一个`slice`方法。这里有一个简单的例子:

```
let myArray = [ '⚡️', '🔎', '🔑', '🔩' ];
let newArray = myArray.slice(2, 3);console.log(newArray); // [ '🔑' ]
```

`slice`方法有两个可选参数`start`和`end`。如果您愿意，您可以两者都提供、只提供`start`，或者都不提供——因此所有这些都是有效的:

```
let arrayOne = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayOneSlice = arrayOne.slice(2, 3);  // [ '🔑' ]let arrayTwo = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayTwoSlice = arrayTwo.slice(2);  // [ '🔑', '🔩' ]let arrayThree = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayThreeSlice = arrayThree.slice();  // [ '⚡️', '🔎', '🔑', '🔩' ]
```

# 开始

这是要包含在新数组中的第一个项目的索引。例如，如果设置为`2`，`slice`将从索引 2 开始新的数组复制。如果使用负数，则表示从序列末尾的偏移量。例如:

```
let arrayOne = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayOneSlice = arrayOne.slice(-2);  // [ '🔑', '🔩' ]
let arrayOneSliceAgain = arrayOne.slice(-1);  // [ '🔩' ]
```

# 结束

这是从切片数组中排除的第一个元素——这有点令人困惑。您可能希望`end`表示最后一个要包含的项目——但是它是第一个要排除的项目。如果你使用`slice`，请记住这一点！如果省略此参数，`slice`方法将简单地继续到数组的末尾，如下例所示:

```
let arrayTwo = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayTwoSlice = myArray.slice(2);  // [ '🔑', '🔩' ]
```

如果使用了大于数组长度的值，`slice`只会继续到数组的末尾。如果使用负值，则表示从数组末尾的偏移量。例如，`(2, -1)`将从数组的开始处为 2，从末尾处为-1:

```
let arrayOne = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayOneSlice = arrayOne.slice(2, -1);  // [ '🔑' ]
let arrayOneSliceAgain = arrayOne.slice(1, -1);  // [ '🔎', '🔑' ]
```

# 使用 slice 制作数组的副本 [#](https://fjolt.com/article/javascript-slice#using-slice-to-make-a-copy-of-an-array)

Slice 不会改变原始数组。相反，它会创建一个新的浅层副本。因此，现有数组仍将继续包含相同的值:

```
let arrayOne = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayOneSlice = arrayOne.slice(2, 3); console.log(arrayOne); // [ '⚡️', '🔎', '🔑', '🔩' ]
console.log(arrayOneSlice); // [ '🔑' ]
```

由于`slice`对数组进行浅层复制，所以它有时也用于复制数组数据。例如，一个空的`slice`函数也将在内存中创建一个新的数组——允许您在内存中拥有同一个数组的两个副本，引用相同:

```
let arrayOne = [ '⚡️', '🔎', '🔑', '🔩' ];
let arrayOneSlice = arrayOne.slice();arrayOneSlice[2] = '⚡️'
console.log(arrayOne); // [ '⚡️', '🔎', '🔑', '🔩' ]
console.log(arrayOneSlice); // [ '⚡️', '🔎', '⚡️', '🔩' ]
```

这在某些情况下很有用。然而，`slice`只是做了一个数组的浅层拷贝。这意味着当数组中有对象时，事情会变得有点混乱。考虑以下阵列:

```
let arrayOne = [ { items: [ '⚡️', '🔎', '🔑', '🔩' ]}, '👨‍💻', '😄', '🐔' ]
```

该数组中包含一个对象。让我们尝试制作这个数组的切片副本，然后更新`items`:

```
let arrayOne = [ { items: [ '⚡️', '🔎', '🔑', '🔩' ]}, '👨‍💻', '😄', '🐔' ]
let arrayOneSlice = arrayOne.slice(0, 2);arrayOneSlice[0].items = [ '🔎' ];
arrayOneSlice[1] = '🔎';console.log(arrayOne); // [ { items: [ '🔎' ]}, '👨‍💻', '😄', '🐔' ]
console.log(arrayOneSlice); // [ { items: [ '🔎' ]}, '🔎' ]
```

等等，什么？我们改变了`arrayOneSlice`的`items`对象，但是它在`arrayOne`和`arrayOneSlice`中都改变了！同时`arrayOneSlice[1]`只改变了`arrayOneSlice`！欢迎来到另一个 Javascript 怪癖。在第一个例子中，使用了`arrayOneSlice[0].items`符号，Javascript 将其解释为更新浅层副本中的现有元素，因此它影响了原始元素。然而，有些令人困惑的是，通过使用`arrayOneSlice[1]`符号，Javascript 将其解释为将新值放入浅层副本本身的`[1]`位置。

这意味着，尽管在处理简单的数组时，看起来像是在用`slice`做一个拷贝，但在处理更复杂的对象时，这并不成立。了解这一点小事，总有一天会为你节省很多时间。

# 结论 [#](https://fjolt.com/article/javascript-slice#conclusion)

Javascript slice 方法对于使用原始数组数据的子集创建新的数组浅层副本非常有用。它还可以以有限的方式用于制作可以独立更新的副本。Javascript 切片副本在内存中仍然具有与原始副本相同的引用，在操作它们时知道这一点很有用。

我希望你喜欢这个指南。[要了解更多 JavaScript，请点击这里查看我的其他文章](https://fjolt.com/category/javascript)。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****