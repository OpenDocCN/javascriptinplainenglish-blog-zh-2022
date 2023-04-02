# 理解 JavaScript 中的浅层和深层拷贝

> 原文：<https://javascript.plainenglish.io/understand-shallow-and-deep-copies-in-javascript-7f8d7d340d48?source=collection_archive---------8----------------------->

![](img/ccf9f0598dcce6db67b81d30d1283d58.png)

Image by [Patryk Kosmider](https://stock.adobe.com/contributor/201245900/patryk-kosmider?load_type=author&prev_url=detail) viaAdobe Stock Photos

JavaScript 中并非所有副本都是相同的。当新开发人员遇到这种情况时，他们可能会感到困惑。当你在 JavaScript 中拷贝一个变量时，它被分为浅层拷贝和深层拷贝。不知道这两者之间的区别或者它们是如何产生的会导致一些混乱的行为。当我第一次开始时，它是许多令人挠头的错误的来源。希望这篇文章能让你避免犯同样的错误。首先，我将介绍一些复制变量的基本示例。

举个例子:

```
let apple = "apple";
let pear = applepear = "pear"console.log("apple: ", apple);
console.log("pear: ", pear);
```

如果您猜测 apple 的输出是“apple ”, pear 是“pear ”,那么您将是正确的。现在我们来看另一个。

```
const fruitStand = {
 apples: 3
}const fruitStandCopy = fruitStand;fruitStandCopy.apples = 7console.log("Fruit Stand: ", fruitStand.apples);
console.log("Fruit Stand Copy: ", fruitStandCopy.apples);
```

你可能认为`fruitStand.apples`的输出是 3，而`fruitStandCopy.apples`的输出是 7。然而，`fruitStand.apples`和`fruitStandCopy.apples`都等于 7。这个行为是 JavaScript 如何处理深层和浅层拷贝的一个例子。

## 记忆

在我们深入研究深层和浅层拷贝之前，我们需要了解内存是如何工作的。当你在 JavaScript 中创建一个变量时，它必须存在于某个地方。它不能只是文件中的一行，它需要被记录下来，以防我们以后要再次引用它。每次你创建一个新变量，它都会在内存中被分配一个空间。

```
const variable1 = "Hello" // memory address: 0x001
const variable2 = 100     // memory address: 0x002
```

上面的两个变量都有单独的空间来存储值。当您稍后在应用程序中引用变量时，您引用的不是创建变量的行，而是存储变量值的内存地址。

```
const variable1 = "Hello" // points to memory address: 0x001
const variable2 = 100     // points to memory address: 0x002console.log(variable1)
```

在上面的例子中，当我们在`console.log`中引用`variable1`时，JavaScript 不会向上 3 行到 variable1 被创建的地方并检查值。它要去与变量 1 相关的内存地址。

## 原语与引用

就深层和浅层复制而言，您可以创建两种变量。第一个是原语，基本的原语类型有字符串、数字、布尔、未定义和空。

```
const name = "Jesse"
const age = 30
```

第二个是引用变量，也称为对象。

```
const person = {
  name: "Jesse",
  age: 30
}
```

我们在浅拷贝和深拷贝的讨论中区分这两者的原因是，当你拷贝一个原始值时，一个新的内存地址被分配给它。当引用变量被复制时，新的变量将指向内存中被复制的变量空间。

```
// primitive value
const name = "Jesse"               // memory address: 0x001// reference value               
const person = { name: "Jesse" }   // memory address: 0x002// primitive copy points to new memory address
const nameCopy = name              // memory address: 0x003// reference copy points to orginial memory address
const personCopy = person          // memory address: 0x002
```

## 浅显的副本

让我们回到这个例子

```
const fruitStand = {
 apples: 3
}const fruitStandCopy = fruitStand;fruitStandCopy.apples = 7console.log("Fruit Stand: ", fruitStand.apples);
console.log("Fruit Stand Copy: ", fruitStandCopy.apples);
```

这是一个浅拷贝的例子。浅表副本指向与原始副本相同的内存空间。

```
const fruitStand = {               // memory address: 0x001
 apples: 3
}fruitStandCopy = fruitStand // memory address: 0x001fruitStandCopy.apples = 7
```

我们现在有两个变量，但都指向内存中的同一个位置。这就是为什么`fruitStand.apples`和`fruitStandCopy.apples`在更新其中一个变量后，值是一样的。当我们改变这个值时，我们改变了存储在这个变量的内存地址中的值。因为两个变量指向同一个地方，所以变化会反映在两者中。

我们所做的并没有什么本质上的错误。这就是 JavaScript 处理复制对象的方式。

## 深层副本

深层副本是不与源变量共享相同引用的副本。这样做的意义在于，一个变量中的更新不会反映在其他变量中。

在前面的例子中，我们看到原始变量在被复制时会获得新的内存地址。这在技术上是深度复制的一个例子，然而，术语深度复制通常是为复制的引用变量保留的。

不幸的是，当我们复制一个引用变量时，我们不会自动得到这种行为。因为无法知道一个对象可能有多大，所以默认情况下 JavaScript 浅层复制对象更有效。

## 创建深层副本

如果您需要创建引用变量的深层副本，可以使用一些技术。

如果您需要复制的对象只有一层深度，我建议使用 spread 操作符进行深度复制。

```
const fruitStand = {
 apples: 3
}
const fruitStandCopy = {...fruitStand};fruitStandCopy.apples = 7console.log(fruitStand.apples)      // 3
console.log(fruitStandCopy.apples)  // 7
```

对于比这更复杂的情况，可以结合使用 JSON.parse()和 JSON.stringify()。

```
const fruitStand = {
 apples: 3
}const fruitStandCopy = JSON.parse(JSON.stringify(fruitStand))fruitStandCopy.apples = 7console.log(fruitStand.apples)      // 3
console.log(fruitStandCopy.apples)  // 7
```

这种技术很危险，因为原始对象内部的函数不会被复制。

也可以使用 lodash 这样的第三方库进行深度复制。如果你在一个大的应用程序中工作，有可能已经为其他方法安装了它。

## 包扎

我希望这篇文章对那些对用 JavaScript 复制变量感到困惑的人有所帮助。看到摆在你面前的行为可能会很奇怪。随着时间的推移，这将成为您的第二天性，您将能够避免浅拷贝和深拷贝对代码库造成的棘手错误。根据我自己的经验，我知道这些可能是最难调试的，你越快记住它们，从长远来看你就越好。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*