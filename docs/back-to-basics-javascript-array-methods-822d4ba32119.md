# 回到基础:JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/back-to-basics-javascript-array-methods-822d4ba32119?source=collection_archive---------17----------------------->

## 解释一些最常见的 Javascript 数组方法，并举例说明如何使用它们。

![](img/72270da9fb79f9f9ee4319edc3de4944.png)

Image by [Goran Ivos](https://unsplash.com/@goran_ivos) via Unsplash

JavaScript 是世界上最常见的编码语言，因此是有抱负的开发人员最需要掌握的语言之一。正如我之前提到的，我目前正在学习 Codecademy 课程，作为其中的一部分，我开始学习 JavaScript。在快速浏览了早期的模块并完成了一些简单的项目后，当所有不同的数组方法被引入时，我的第一个挑战就来了。

有很多内容解释了不同的方法，但在本文中，我打算在一个地方进行总结，并概述如何以及为什么使用它们。

# 。地图()

[map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 将一个函数应用于整个数组，然后返回一个包含修改后元素的新数组。(如果您想覆盖值而不在代码中构建太多变量，也可以重新分配原始数组)。

```
let myArray = [1, 2, 3, 4];let newArray = myArray.map(num => num * 2)console.log(newArray) **//returns [2, 4, 6, 8]**
```

# 。forEach()

[forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) 是在处理数组时编写 for 循环的精简方法。该方法将对数组的每个元素进行循环，并执行一个函数。值得注意的一点是，它不返回任何内容，因此将输出记录到控制台将返回“未定义”。

```
let myArray = [1,2,3]
myArray.forEach(num => console.log(num));**//Returns:
// 1
// 2
// 3**
```

# 。减少()

在所有的数组方法中 [reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) 最让我困惑。该方法将按顺序对所有元素执行一个函数，将返回值重新输入到下一个循环中。一个简单的方法是对数组的所有值求和(这是我下面代码片段中的第一个例子)。

reduce 方法还接受一个附加参数，该参数可以放在函数计算之后。这是初始值输入(在下面的第三个示例中用数字 100 表示)。当给定初始值时，该方法将从这个数字开始第一次循环，并用这个初始值和数组中的第一个元素执行函数。

还在迷茫？希望下面的三个例子展示了这种应用的不同方式，有助于澄清这一切…

```
//Example 1: Sum up all array elements
let myArray = [1,2,3];@
let result = myArray.reduce((previous,current)=>previous+current);
console.log(result); //returns 6//Example 2: Subtract all elements from the first elementlet newArray = [10,3,2];
let newResult = newArray.reduce((previous,current)=>previous-current);
console.log(newResult); //returns 5//Example 3: Starting from 100 subtract all elementslet finalArray = [10,5,5];
let finalResult = finalArray.reduce((previous,current)=>previous-current,100);
console.log(finalResult); //returns 80
```

# 。每隔()

[every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) 对数组中的元素进行测试。如果所有元素都通过，那么它将返回“真”，但是如果一个(或多个)元素不符合标准，那么将返回“假”值。当试图检查整个数组是否在限制范围内时，这是很有用的—例如，在下面的代码片段中，我们试图检查一组考试分数是否合理，并且没有学生得分超过 100%(这是不可能的，表明存在标记错误)。

```
let examScore= [90,32,56,102,89];let result = examScore.every(num => num < 100);console.log(result);  **//returns: false**//let newExamScore= [90,32,56,75,89];let newResult = newExamScore.every(num => num < 100);console.log(newResult);  **//returns: true**
```

# 。一些()

[some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some) 的工作方式与 every()类似，对数组中的所有元素进行测试。不同之处在于，如果任何元素满足标准，将返回 true 值。所有元素都需要在函数标准之外，这样它才能返回值 false。

```
let myArray = ["cat","dog","pig"];let result = myArray.some(animal => animal.length > 3);console.log(result) **//returns false**//let newArray = ["cat","fish","pig"];let newResult = newArray.some(animal => animal.length > 3);console.log(newResult) **//returns true**
```

# 奖金方法

这些并没有出现在我的文章中，因为它们是我第一次学习的方法，但是把它们排除在外是一种疏忽，所以我在下面做了一个简短的概述:

*   [**pop()**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) —删除数组中的最后一个元素。
*   [**【push()**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)—将一个或多个元素添加到数组末尾。例如，对数组调用 myArray.push("cake ")会将元素 cake 添加到已经存储在 myArray 中的内容的末尾。
*   [**shift()**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) —从数组中删除第一个元素。
*   [**【un shift()**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)**—将一个元素添加到数组的开头。例如，在数组上调用 myArray.push("dog ")会在 myArray 中已经存储的任何元素前面添加元素" dog "。**
*   **[**【fill()**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)**—当您想要用固定值覆盖数组值时，这可能很有用。可以输入 3 个参数—第一个指定要输入的值，第二个指定开始填充的元素，第三个指定停止填充的值。如果参数 3 丢失，数组将被填充到末尾(如果参数 2 也丢失，整个数组将被指定的值替换)。例如，如果 myArray=[1，2，3，4]并且您调用 myArray.fill(0，1，2)，则结果将是 myArray=[1，0，0，1]。****

****我希望这对你有用，并以一种可理解的方式解释了一些最常见的数组方法。如果你觉得它有用或者认为我错过了其他的，请告诉我！****

> ****如果你喜欢这篇文章，并想阅读更多，一定要查看我的类似文章。考虑成为一个媒体成员，以获得无限的接触最好的想法和作家。****
> 
> ****如果你通过这个链接加入 Medium，我会从你的费用中收取很少的一部分——而且不会花你任何额外的费用！提前感谢。 **💰******
> 
> *****感谢阅读！*****

*****更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*****