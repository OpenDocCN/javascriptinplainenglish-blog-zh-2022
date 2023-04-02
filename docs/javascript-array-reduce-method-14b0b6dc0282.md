# JavaScript“array . reduce()”方法是什么

> 原文：<https://javascript.plainenglish.io/javascript-array-reduce-method-14b0b6dc0282?source=collection_archive---------12----------------------->

## reduce()方法用于处理一个数组，并基于数组中的所有元素返回值——下面是 reduce()方法的工作原理。

![](img/49144efc8a9b7b5f054b96397cce4fb4.png)

JavaScript reduce 方法是一种递归方式，它基于数组中的每个元素执行计算，同时还考虑数组中的前一个元素。它接受一个函数，该函数也可用于根据您选择的逻辑进一步处理数组元素。

这是非常有用的求和数组，或合并字符串为基础的数组。例如，我们可以将一个数组转换成一个字符串，如下所示:

```
let myArray = [ 'hello', 'world', 'welcome!' ]let reduceString = myArray.reduce((previousElement, currentElement) => {
    return `${previousElement} ${currentElement}`;
})console.log(reduceString); // hello world welcome!
```

同样，我们可以用它将数组中的所有数字相加，并返回一个数字:

```
let myArray = [ 5, 10, 15, 20 ]let reduceString = myArray.reduce((previousElement, currentElement) => previousElement + currentElement)console.log(reduceString); // 50
```

# reduce 方法回调函数

reduce 中使用的回调函数实际上有 4 个参数。您不需要使用任何一个，但是前两个是您通常想要的。该函数的格式如下所示:

```
Array.reduce((previousElement, currentElement, currentIndex, array) => {
    // Do something with the array's data
}, initialValue)
```

我们来看看`previousElement`、`currentElement`、`currentIndex`、`array`、`initialValue`都是什么意思。

# 前一元素

这是不言自明的。它表示我们正在迭代的当前元素的前一个元素。`reduce`函数通常会从索引`[1]`开始，因此前一个元素确实存在。如果您已经定义了一个`initialValue`，那么将使用这个值，并且`reduce`函数将从索引`[0]`开始，使用`initialValue`作为`previousValue`。

# 电流遥测

这是 reduce 正在迭代的当前元素。

# currentIndex

因为数组不仅仅由索引组成，而且通常包含有用的数据，所以我们也有能力获取正在迭代的当前索引。这将返回表示当前元素在数组中位置的 0 索引数字。期望从该参数得到标准数组索引。

# 排列

这将返回整个数组——如果您计划使用`reduce`操作数组，或者如果您想要基于数组中的其他元素进行计算，这将非常有用

# 初始值

如果提供，这将是索引`[0]`的`previousElement`。

如上所述，这些都是可选的，但是它们都提供了一种有用的方式来操作和计算您的`reduce`方法的返回值。

# 在 reduce 中变异数组

如果你试图改变`reduce`中的数组，可能会导致一些有趣的行为——所以在考虑`reduce`时，你应该考虑一些边缘情况。

例如，如果您在当前元素之前的某个位置更改了数组元素，则归约仍会按预期进行。例如，将`1000`加到`myArray[currentIndex + 1]`仍会产生预期值:

```
let myArray = [ 4, 5, 6, 7, 8 ]
let reduceFunction = myArray.reduce((prevValue, currentValue, currentIndex) => {
    myArray[currentIndex + 1] += 1000
    return prevValue + currentValue
});
console.log(reduceFunction); // 3030
```

**然而**，试图在运行`reduce`的时候给一个数组加值是行不通的。例如，下面我使用`push`为数组中的每个元素添加一个元素。这当然会导致一个无限循环，所以 Javascript 停止这个函数，只处理我们运行`reduce`时数组中的值:

```
let myArray = [ 4, 5, 6, 7, 8 ]
let reduceFunction = myArray.reduce((prevValue, currentValue, currentIndex) => {
    myArray.push(1000)
    return prevValue + currentValue
});
console.log(reduceFunction); // 30
```

# 关于单值数组的注记

如果你的数组只包含一个值，并且你没有使用`initialValue`，那么`reduce`函数将从数组中返回一个值，并且不调用回调函数。例如:

```
let myArray = [ 'cat' ]
let reduceFunction = myArray.reduce((prevValue, currentValue) => {
    return currentValue + '!'
});
console.log(reduceFunction); // cat (does not have exclamation mark, even though we tried to add it)
```

# 对对象数组中的值求和并组合

您可能已经预料到了这种行为，但是如果您有一个对象数组，您可以引用每个 elements 对象的子属性来进行计算。例如，将下面所有的`age`相加:

```
let myArray = [ { age: 52 }, { age: 34 }, { age: 104 }, { age: 29 } ]
let reduceFunction = myArray.reduce((prevValue, currentValue) => {
    return prevValue + currentValue.age
}, 0);
console.log(reduceFunction); // 219
```

您可能已经注意到了这里的一些奇怪的事情，这就是为什么研究这个例子是有用的:

*   我们必须定义一个`initialValue`，因为最初，`prevValue`是`{ age: 52 }`，但后来，`prevValue`是一个`number`。这意味着我们保持类型一致。
*   因为每次我们运行`reduce`时，它都返回数组元素中当前项的 a 值，所以我们使用`prevValue`而不是`prevValue.age`。`prevValue.age`未定义，因为`reduce`每次返回一个数字。

# 结论

方法`reduce`是一种非常有用的方法，可以组合数组中的所有内容，或者生成您选择的新数组。它很强大并且是递归的，所以在大型数据集上使用时要小心。如果你喜欢这个，我也在这里写了一篇关于切片法的文章。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***