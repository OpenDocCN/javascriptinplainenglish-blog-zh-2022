# 如何自己实现 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/how-to-implement-javascript-array-methods-by-yourself-e06b976ca4c0?source=collection_archive---------12----------------------->

## 映射，归约，筛选，forEach，查找，每

![](img/d3836ad6a16ae6acccec948603eb7e14.png)

Photo by [Yifu Wu](https://unsplash.com/@nnonno?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/array-methods?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我们都用类似 ***的数组方法。地图，。forEach，。过滤器，。减少*** 。作为参数，它们总是接受一个函数，该函数又接受不同数量的参数。我一直想知道它们是如何实现的，但是一直没有时间去弄清楚，直到有一天在一次面试中，我被要求写一个数组方法的实现。从理论上讲，这并不难，但在实践中，事实证明这有点难。因此，在本文中，我们将分析我们的主要数组方法的实现。

***。* forEach**

此方法的语法如下:

```
arr.forEach(function(currentValue, index, array) {
    //your iterator
},thisArg);
```

因此，根据语法，我们的方法必须有两个参数，我们将传递数组元素的函数: *index* ，整个数组。第二个参数是一个值，当在函数内部调用时，该值将等于这个值，但是这对于 arrow 函数不起作用，因为它们没有自己的上下文。

> 此外，我们不会显示对函数类型的检查，因为它对我们将要考虑的所有方法都是一样的。

## ***。*地图**

此方法的语法如下:

```
const newArr = arr.map(function(currentValue, index, array){ 
   //your iterator
}, thisArg)
```

因此，根据语法，我们的方法类似于前一个方法，但返回一个新的数组

## ***。过滤器***

此方法的语法如下:

```
const newArr = arr.map(function(currentValue, index, array){ 
   //your iterator
}, thisArg)
```

因此，根据语法，我们的方法将那些不为空的元素写入新数组，并且函数调用返回真值

## 。减少

此方法的语法如下:

```
const result = arr.reduce(function(accumulator, element, index, array){
    //your iterator
}, initialAccumulator])
```

因此，根据语法，我们的方法在迭代完数组中那些 ***不为空的*** 元素后，返回 ***累加的*** 值

## 。发现

此方法的语法如下:

```
const result = arr.find(function(currentValue, index, array) {
    //your iterator
},thisArg);
```

所以，根据语法，我们的方法返回数组的 ***元素*** 如果调用的函数返回 true 否则返回 ***未定义的***

## 。每个

此方法的语法如下:

```
const boolean = arr.every(callback(currentValue, index, array){
   //your iterator
}, thisArg)
```

当然，这个实现不会取代内置的方法，因为有很多检查，但是显示了构建您自己的方法的一般原则。

希望对你有用！

感谢阅读！回头见。😊

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****