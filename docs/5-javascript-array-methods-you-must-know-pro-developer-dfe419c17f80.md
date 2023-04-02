# 5 JavaScript 数组方法你必须知道| Pro 开发者

> 原文：<https://javascript.plainenglish.io/5-javascript-array-methods-you-must-know-pro-developer-dfe419c17f80?source=collection_archive---------2----------------------->

## 这里有五个 JavaScript 数组方法，每个开发人员都应该知道。

下面是`map()`方法的语法:

```
const newArray = array.map(function(currentValue, index, array) { // Return element for newArray });
```

`map()`方法采用回调函数作为参数，该参数应用于数组的每个元素。回调函数有三个参数:

*   `currentValue`:数组中当前正在处理的元素。
*   `index`(可选):数组中当前正在处理的元素的索引。
*   `array`(可选):召唤`map()`的阵。

`map()`方法返回一个新的数组，因此它不会修改原始数组。

下面是如何使用`map()`对数组元素进行平方的示例:

```
const array = [1, 2, 3]; const squaredArray = array.map(x => x * x); console.log(squaredArray); // [1, 4, 9]
```

下面是`filter()`方法的语法:

```
const newArray = array.filter(function(currentValue, index, array) { // Return true if element should be included in newArray, false otherwise });
```

`filter()`方法将回调函数作为参数，应用于数组的每个元素。回调函数有三个参数:

*   `currentValue`:数组中当前正在处理的元素。
*   `index`(可选):数组中当前正在处理的元素的索引。
*   `array`(可选):调用`filter()`的数组。

`filter()`方法返回一个新的数组，因此它不会修改原始数组。

下面是如何使用`filter()`从数组中获取偶数的示例:

```
const array = [1, 2, 3, 4, 5, 6]; const evenNumbers = array.filter(x => x % 2 === 0); console.log(evenNumbers); // [2, 4, 6]
```

下面是`reduce()`方法的语法:

```
const reducedValue = array.reduce(function(accumulator, currentValue, currentIndex, array) { // Return updated accumulator value }, initialValue);
```

`reduce()`方法将回调函数作为参数，应用于数组的每个元素。回调函数有四个参数:

*   `accumulator`:累加器累加回调的返回值。它是上次调用回调时返回的累计值，或者是初始值(如果提供)。
*   `currentValue`:数组中当前正在处理的元素。
*   `currentIndex`(可选):数组中当前正在处理的元素的索引。
*   `array`(可选):召唤阵`reduce()`。

`reduce()`方法还有一个可选的`initialValue`参数，可以用来指定累加器的初始值。如果没有提供初始值，数组中的第一个元素将被用作初始值，回调将应用于剩余的元素。

下面是一个如何使用`reduce()`来计算数组总和的例子:

```
const array = [1, 2, 3, 4, 5]; const sum = array.reduce((accumulator, currentValue) => accumulator + currentValue, 0); console.log(sum); // 15
```

下面是`sort()`方法的语法:

```
const sortedArray = array.sort(function(a, b) { // Return 0 if a and b should be left unchanged, a negative value if a should come before b, or a positive value if b should come before a });
```

`sort()`方法将一个可选的比较函数作为参数，用于确定元素的顺序。compare 函数有两个参数:`a`和`b`，它们代表被比较的两个元素。

默认情况下，`sort()`方法根据元素的 Unicode 码位对元素进行升序排序。但是，您可以指定一个自定义的比较函数，以不同的顺序对元素进行排序。

下面是一个如何使用`sort()`对数字数组进行升序排序的例子:

```
const array = [3, 2, 1]; const sortedArray = array.sort((a, b) => a - b); console.log(sortedArray); // [1, 2, 3]
```

下面是`reverse()`方法的语法:

```
const reversedArray = array.reverse();
```

`reverse()`方法没有任何参数，也没有返回值。它只是颠倒了原始数组中元素的顺序，并返回颠倒的数组。

下面是一个如何使用`reverse()`反转数组中元素顺序的例子:

```
const array = [1, 2, 3]; const reversedArray = array.reverse(); console.log(reversedArray); // [3, 2, 1]
```

*原载于 2022 年 12 月 26 日 https://coderfact.com*[](https://coderfact.com/code-snippets/5-javascript-array-methods-you-must-know-pro-developer/)**。**

**更多内容请看* [***说白了就是***](https://plainenglish.io/) *。**

**报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **

*****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。***