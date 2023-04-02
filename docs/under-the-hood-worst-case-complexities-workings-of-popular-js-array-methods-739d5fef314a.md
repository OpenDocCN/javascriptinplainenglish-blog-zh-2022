# 引擎盖下:最坏情况的复杂性&流行的 JS 数组方法的工作方式

> 原文：<https://javascript.plainenglish.io/under-the-hood-worst-case-complexities-workings-of-popular-js-array-methods-739d5fef314a?source=collection_archive---------1----------------------->

## 概述:了解流行的 JS 数组方法以及它们是如何工作的。

![](img/37257040d945c80cc97c11d64bd6ea67.png)

Photo by [Joan Gamell](https://unsplash.com/@gamell?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/js?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 概述:

1.  介绍
2.  大 O 符号和工作方法如下:

*。在()，。copyWithin()，。concat()，。条目()，。every()，。fill()，。find()，。filter()，。forEach()，from()，includes()，indexOf()，。map()，。reduce()，… (spread 运算符)，shift()，some()，slice()，splice()，sort()，push()，pop()，。toString()，unshift()，values()*

*需求——大 O 符号，JS 数据结构。*

*级别—中级*

# 简介:

对于所有 JS 开发人员来说，无论您是专业人员还是试图破解令人恐惧的编码面试，都可以使用内置数组方法。filter()，。reduce()，。map()等。是我们的第二天性。

这些方法引入了一个抽象层次，使得代码更容易阅读，编写起来更简单快捷。

但是你有没有想过这种方法最糟糕的时间和空间复杂性(大 O)是什么，或者它们是如何工作的？它们可能看起来像简单的一行程序，但是很多都隐藏在里面。

在本文中，我们将深入研究这些方法的幕后工作和效率。

# 在我们继续之前…

任何数组操作都没有指定的*时间*复杂度保证。数组的性能取决于引擎选择的底层数据结构。引擎也可能有不同的表示，并根据特定的启发在它们之间切换。[4]

数组操作几乎总是根据它所代表的运行时引擎进行优化。

***因此*** *，这篇文章概述了如果不进行优化，这些数组方法的空间和时间复杂性是什么，以及用来表示它们的底层数据结构是一个数组。*

# 。在()

`**at()**`方法接受一个整数值，并返回正整数的索引项。对于负整数，从数组的最后一项开始计数。[6]

## 大 O:

时间复杂度— ***O(1)***

方法不会循环访问数组来获取元素。它使用直接给出的索引。

空间复杂性— ***O(1)***

此方法从数组中返回单个元素。

# 。copyWithin()

`**copyWithin()**`方法将数组的一部分复制到同一个数组中的另一个位置，并在不修改其长度的情况下返回它。[5]

**大 O:**

时间复杂度— ***O(n)***

这种方法类似于 C++的`**memmove**`**【5】用来移动数组中的数据。在最坏的情况下，n-1 个元素将被复制到数组中的新位置。**

**空间复杂性— ***O(1)*****

**所有修改都已就绪，修改后将返回原始数组。**

# **。concat()**

**`**concat()**`方法用于合并两个或多个数组，返回一个浅拷贝的新数组。[7]**

## **大 O:**

**时间复杂度— ***O(n)*****

**当两个数组被*合并*时，该操作将考虑合并最大列表所花费的时间。**

**空间复杂性— ***O(n)*****

**此方法的结果是两个数组的浅表副本。因此，空间复杂度为 O(n)。**

# **。条目()**

**`**entries()**`方法返回一个新的数组迭代器对象，它包含数组中每个索引的键/值对。[19]**

## **大 O:**

**时间复杂度— ***O(n)*****

**所有的元素都必须被线性扫描，并且在迭代器对象中包含一个数组[index，element]。**

**空间复杂性— ***O(n)*****

**返回一个新的迭代器对象，其中包含每个元素的数组。单个数组具有恒定的间距。**

# **。每隔()**

**`**every()**`方法测试数组中的所有元素是否通过由提供的函数实现的测试，并返回一个布尔值。[20]**

## **大 O:**

**时间复杂度— ***O(n)*****

**在最坏的情况下，所有的元素都被扫描并对照测试进行检查。**

**空间复杂性— ***O(1)*****

**该方法返回一个布尔值。**

# **。填充()**

**`**fill()**`方法将数组中的所有元素更改为给定的静态值，从起始索引(默认为`0`)到结束索引(默认为`array.length`)，并返回修改后的数组。[21]**

## **大 O:**

**时间复杂度—**

***该阵列的所有元素可以在线性时间内改变。***

***空间复杂度— ***O(1)******

***方法返回修改后的数组。***

# ***。过滤器()***

***`**filter()**`方法创建了一个*浅拷贝*，它包含了所有通过过滤函数的元素。[22]***

***In this example, the new ‘result’ array contains element which are greater than 4.***

## ***大 O:***

***时间复杂度— ***O(n)******

***线性地对数组*的所有元素执行回调函数，分别检查它们是否通过测试。****

****空间复杂度— ***O(n)*******

****filter 方法的结果存储在一个新数组中。在最坏的情况下，所有元素都可能通过测试，因此，空间将等于输入数组的大小。****

******注:** *浅拷贝是与源有相同引用的拷贝。这意味着对新拷贝的任何更改也会反映在源代码中。例如:在上面的例子中，从“结果”数组中删除值 6 也会将其从“值”数组中删除。*****

# ****。查找()****

****`**find()**`方法返回所提供的数组中满足所提供的测试函数的第一个元素。[23]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****测试函数可能必须在线性时间内检查数组的所有元素。****

****空间复杂性—***O①*******

****通过测试的第一个元素从数组中返回。****

# ****。forEach()****

****`**forEach()**`方法为每个数组元素执行一次提供的函数。[24]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****回调函数线性地在数组*的所有元素上实现，并且就地进行改变。*****

*****空间复杂性— ***O(1)********

****在所有元素都经历了回调函数之后，返回相同的数组，因此没有使用额外的空间。****

# ****。来自()****

*****Array . from()**static*方法从可迭代或类似数组的对象(如字符串、数组、映射或集合)创建一个新的、空拷贝的*数组实例。[25]*****

****Here, the string ‘abcd ef gh’ is converted to an array with each letter as an element. In the second example, a call back function is implemented to increment every element by 1.****

## ****大 O:****

****时间复杂度— ***O(n)*******

****回调函数线性地在数组*的所有元素上实现，并且就地进行更改。*****

*****空间复杂度— ***O(n)********

****创建一个新的元素数组，它使用的空间与输入的类似数组的对象大约相同。****

# ****。包括()****

****`**includes()**`方法检查数组中是否存在一个值或元素，并分别返回*真*或*假*。[26]****

****Here, string ‘c’ exists in arr2 hence output is the boolean value true whereas string ‘z’ does not which is false.****

## ****大 O:****

****时间复杂度— ***O(n)*******

****在最坏的情况下，该方法必须迭代并检查数组中的所有值。****

****空间复杂性— ***O(1)*******

****该方法返回布尔值 true 或 false，这不需要额外的空间。****

# ****。索引 Of()****

****`**indexOf()**`方法返回给定元素在数组中的第一个索引，如果不存在则返回-1。[18]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****该方法必须在最坏的情况下解析所有元素，以确定该元素是否存在。****

****空间复杂性— ***O(1)*******

****方法返回元素的索引或-1。****

# ****。加入()****

****`**join()**`方法通过连接一个数组中的所有元素(或一个类似于[数组的对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#working_with_array-like_objects))创建并返回一个新的字符串，用逗号或指定的分隔符字符串分隔。[17]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****为了创建字符串，必须对所有元素进行线性解析。****

****空间复杂度— ***O(n*m)*******

****该方法返回一个字符串，其中 n 是节点数，m 是最大字符串的长度。****

# ****。地图()****

****`**map()**`方法创建一个新的数组，用调用数组中每个元素的函数的结果填充。****

## ****大 O:****

****时间复杂度— ***O(n)*******

****这种方法利用一个回调函数来单独和线性地处理每个元素，并存储在新的数组中。****

****空间复杂性— ***O(n)*******

****方法使用回调函数修改的原始数组的值创建一个新数组。****

# ****。减少()****

****`**reduce()**`方法在数组的每个元素上执行一个回调函数，称为“reducer ”,方法是传递前一个元素计算的返回值。对数组的所有元素运行缩减器的最终结果是一个值。****

****Here, the previousValue (return value from calculation of preceding element) is added to the current element and returned. All the elements in the above array are added.****

## ****大 O:****

****时间复杂度— ***O(n)*******

****该方法通过对每个元素逐一运行回调函数来返回累积计算值。****

****空间复杂性— ***O(1)*******

****该方法从所有元素的累积计算中返回一个值。****

# ****…(扩展语法)****

****spread 语法(`...`)允许在零个或多个参数(用于函数调用)或元素(用于数组文字)的地方扩展 iterable，如数组或字符串。****

## ****大 O:****

****时间复杂度—****

*****对于数组，它连续调用数组迭代器的`.next()`方法，直到迭代器用尽。*****

*****空间复杂度— ***O(n)********

*******O(n) - >*** 如果像上面的例子那样在创建新数组时使用，spread 语法将创建原始数组的深层副本。****

*******O(1) - >*** 如果仅用于迭代数组或将参数传递给函数。****

# ****。一些()****

****`**some()**`方法测试*数组中是否至少有一个*元素通过了由提供的函数实现的测试(回调 Fn ),如果是则返回 true，否则返回 false。****

****Here .some() checks if at least 1 element in the array is odd and returns true****

## ****大 O:****

****时间复杂度—****

*****这个方法 ***线性地*** 遍历数组，看看是否至少有一个元素匹配测试。在最坏的情况下，它必须检查所有的元素。*****

****空间复杂性— ***O(1)*******

****该方法返回一个布尔值。****

# ****。推送()****

****`**push()**`方法将一个或多个元素添加到数组的末尾，并返回数组的新长度。****

****The element is inserted in the back of the array. So, [0, -1, 2, 8] becomes [0, -1, 2, 8, -5].****

## ****大 O:****

****时间复杂度— ***O(1)*******

****此方法直接利用当前长度属性向数组末尾添加一个元素，并将长度增加 1。****

****空间复杂性— ***O(1)*******

****方法返回数组的更新长度。****

# ****。流行()****

****`**pop()**`方法从数组中移除最后一个**元素并返回该元素。此方法更改数组的长度。******

## ****大 O:****

****时间复杂度— ***O(1)*******

****此方法直接利用当前长度属性将元素移至数组末尾，并将长度减 1。****

****空间复杂度— ***O(1)*******

****方法返回数组中移除的元素。****

# ****。反向()****

****`**reverse()**`方法就地反转一个数组。第一个数组元素成为最后一个，最后一个数组元素成为第一个。[16]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****阵列的第一个和最后一个元素的交换线性进行，直到阵列反转。****

****空间复杂度— ***O(1)*******

****该方法就地反转占用恒定空间的数组。****

# ****。shift()****

****方法从数组中移除第一个元素并返回移除的元素。[15]****

****时间复杂度— ***O(n)*******

****为了从数组的开始移除一个元素，所有随后的元素必须相应地移位。****

****空间复杂度— ***O(1)*******

****返回移除的元素。****

# ****。切片()****

****`**slice()**`方法将数组的一部分的浅拷贝返回到从*开始*索引到*结束*索引选择的新数组对象中。原始数组不会被修改。[14]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****如果必须访问所有元素，那么对浅层副本的写入将是线性的。****

****空间复杂性— ***O(n)*******

****如果没有给定索引，则返回数组的一个新的浅表副本。****

# ****。排序()****

****`**sort()**`方法对一个数组的元素进行就地排序，并返回对同一个数组的引用，现在已经排序了。[12]****

## ****大 O:****

****时间复杂度—***(nlogn)*******

****对于较大的数组，快速排序通常用于对数组进行排序。[13]****

****空间复杂度— ***O(logn)*******

****快速排序需要 logn 堆栈空间来实现排序。****

# ****。拼接()****

****`**splice()**`方法通过移除或替换现有元素和/或在适当的位置添加新元素来改变数组的内容。[11]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****在最坏的情况下，如果向阵列中添加一个元素，则必须移动 n-1 个元素。****

****空间复杂性—***O(n+k)~ O(n)*******

****如果将 k 个元素添加到数组中，那么新的长度将是以前的长度+ k ~ n。****

# ****。toString()****

****`**toString()**`方法返回一个代表指定数组及其元素的字符串。[10]****

## ****大 O:****

****时间复杂度—***【O(n)*******

****为了创建字符串，必须对所有元素进行线性解析。****

****空间复杂度— ***O(n*m)*******

****该方法返回一个字符串，其中 n 是节点数，m 是最大字符串的长度。****

# ****。未移位()****

****`**unshift()**`方法将一个或多个元素添加到数组的开头，并返回数组的新长度。[9]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****为了在数组的开头添加一个元素，所有后续的元素都必须相应地移位。****

****空间复杂性— ***O(n + k) ~ O(n)*******

****在数组中，k 个新元素与前 n 个元素一起添加。****

# ****。值()****

****`**values()**`方法返回一个新的数组迭代器对象，它包含数组中每个索引的值。[8]****

## ****大 O:****

****时间复杂度— ***O(n)*******

****所有元素都必须线性添加到对象中。****

****空间复杂度— ***O(n)*******

****该方法返回一个数组迭代器对象，它包含数组的所有元素。****

# ****结论:****

****在本文中，我们看到了最坏情况下的时间和空间复杂性，以及 JS 数组方法的幕后工作。****

****下次见。干杯！****

# ****参考资料:****

1.  ****[MDN 网络文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/@@iterator)****
2.  ****[时间复杂度大 0 的 Javascript 数组方法及实例。](https://dev.to/lukocastillo/time-complexity-big-0-for-javascript-array-methods-and-examples-mlg)****
3.  ****[大 O 批注](https://medium.datadriveninvestor.com/big-o-notation-14fa1e4538a1)****
4.  ****[Javascript 数组的大 O。](https://stackoverflow.com/questions/11514308/big-o-of-javascript-arrays/61713477#61713477)****
5.  ****[copy within()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin)****
6.  ****[at()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/at)****
7.  ****[concat()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)****
8.  ****[数值()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/values)****
9.  ****[unshift()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)****
10.  ****[toString()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString)****
11.  ****[拼接()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)****
12.  ****[sort()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)****
13.  ****[V8 中的大 O 实现 sort()](https://blog.shovonhasan.com/time-space-complexity-of-array-sort-in-v8/)****
14.  ****[切()法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)****
15.  ****[shift()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)****
16.  ****[反向()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)****
17.  ****[join()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)****
18.  ****[indexOf()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)****
19.  ****[条目()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)****
20.  ****[every()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)****
21.  ****[fill()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)****
22.  ****[过滤()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)****
23.  ****[查找()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)****
24.  ****[forEach()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)****
25.  ****[从()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)****
26.  ****[包括()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)****

*****更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*****