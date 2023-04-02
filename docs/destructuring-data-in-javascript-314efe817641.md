# 如何在 JavaScript 中析构数据

> 原文：<https://javascript.plainenglish.io/destructuring-data-in-javascript-314efe817641?source=collection_archive---------10----------------------->

## 什么是解构数据，如何使用它？

![](img/76db4454ccbd9cd70204b7108ccfc009.png)

Photo by [Iker Urteaga](https://unsplash.com/@iurte?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你读过我的关于 spread 和 rest 语法的故事，你会记得它是用来“扩展”变量或参数的，参数的个数是不确定的。在某种程度上，解构是相反的。它允许您通过分解数据，只提取需要的数据来创建特定的数据集合。析构可用于数组、对象或两者的某种组合。

# 解构数组

析构数组最基本的用途是将数组的单个值赋给它们自己的变量。考虑下面的例子:

```
let colors = ['green', 'orange', 'yellow'];
const [colorA, colorB, colorC] = colors;
console.log(colorA); // 'green'
console.log(colorB); // 'orange'
console.log(colorC); // 'yellow'
```

从包含三个字符串的原始数组`colors`中，我们可以对其进行析构，以便将这三个项目分配给它们自己的变量`colorA`、`colorB`和`colorC`。这也可以用比数组值更多或更少的变量来实现，任何没有被赋予数组值的变量都将是`undefined`:

```
let colors = ['green', 'orange', 'yellow'];
const [colorA, colorB, colorC, colorD] = colors;
console.log(colorA); // 'green'
console.log(colorB); // 'orange'
console.log(colorC); // 'yellow'
console.log(colorD); // undefined
```

如果您想防止未定义的变量，您也可以为它们分配一个默认值:

```
let colors = ['green', 'orange', 'yellow'];
const [colorA='blue', colorB, colorC, colorD='purple'] = colors;
console.log(colorA); // 'green'
console.log(colorB); // 'orange'
console.log(colorC); // 'yellow'
console.log(colorD); // 'purple'
```

析构也可以应用于从函数返回的数组，它们甚至可以被格式化为忽略某些索引:

```
function giveColors() {
    return ['green', 'orange', 'yellow'];
}const [colorA, , colorB] = giveColors();
console.log(colorA); // 'green'
console.log(colorB); // 'yellow'
```

使用析构时容易犯的一个错误是忘记了`const [colors] = giveColors()`将只捕获返回的数组中的第一个元素，而`const colors = giveColors()`将捕获整个数组。

析构也可以与 rest 语法结合使用来捕获数组的剩余部分:

```
function giveColors() {
    return ['green', 'orange', 'yellow'];
}const [colorA, ...colors] = giveColors();
console.log(colorA); // 'green'
console.log(colors); // ['orange', 'yellow']
```

# 解构对象

可以通过析构来操作对象，方法与数组非常相似:

```
const color = {
    name: 'Orange',
    isPrimary: false
};

let {name, isPrimary} = color;

console.log(name); // 'Orange'
console.log(isPrimary); // false
```

它还可以用于重新分配属性名称:

```
let coord = {x: 60, y: 12};
const {x: a, y: b} = coord;console.log(a); // 60
console.log(b); // 12
```

使用重新分配并提供默认值，我们可以做到以下几点:

```
let coord = {x: 60, y: 12};
const {x: a=1, y: b=1, z: c=1} = coord;console.log(a); // 60
console.log(b); // 12
console.log(c); // 1
```

对象甚至可以解包到函数参数中，允许它们被重命名或按原样传递:

```
function outputCoords({x, y, z:height}){
    console.log("Located at "+x+", "+y+" at a height of "+height);
}const loc = {x: 12, y: 15, z: 4};
outputCoords(loc); // Located at 12, 15 at a height of 4;
```

当然，您可以如上所示为这些参数提供默认值，甚至可以嵌套对象和数组以增加复杂性。与数组一样，rest 操作符可用于捕获一组属性:

```
let loc = {x: 60, y: 12, z: 4, time: '0850', duration: 0.42};
let {x, y, z:height, ...extras} = loc;
console.log(x); // 60
console.log(y); // 12
console.log(height); // 4
console.log(extras); // {time: '0850', duration: 0.42}
```

在上面的例子中，`x`和`y`被原样捕获，`z`被重命名为`height`，其余的属性使用 rest 操作符存储在`extras`中。

析构的应用是无限的。我希望你和我一样，掌握这些新知识，并将其应用到未来的项目中。

## **延伸阅读:**

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) [## 析构赋值- JavaScript | MDN

### 析构赋值语法是一个 JavaScript 表达式，它使得从数组中解包值成为可能，或者…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。**