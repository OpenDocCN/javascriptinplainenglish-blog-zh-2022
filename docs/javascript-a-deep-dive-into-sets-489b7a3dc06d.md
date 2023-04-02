# JavaScript:对集合的深入探究

> 原文：<https://javascript.plainenglish.io/javascript-a-deep-dive-into-sets-489b7a3dc06d?source=collection_archive---------11----------------------->

![](img/4108a5df7cb559529e8e11ec41a613b1.png)

# 布景太棒了

前段时间偶然发现 ***JavaScript 集合*** 开始喜欢上了。我也发现自己不只在一个场合需要它。在这篇文章中，我将尝试涵盖为什么我认为 ***集*** 很棒，以及如何利用它们。

我将介绍:

*   什么是集合以及如何创建集合
*   用集合查找特定元素
*   获取集合的大小
*   用集合过滤掉数组中的重复值
*   环
*   集合与阵列的性能

# 什么是集合

`*Sets*` 是一种新的对象类型，可以在 ES6 中使用。集合允许您创建唯一值的集合，并且像数组一样是可迭代的。集合可以保存简单的原语、字符串等值，也可以保存对象文字或数组。

**官方对集合的描述是:** `*Set*` *对象是值的集合。您可以按插入顺序循环访问集合中的元素。* `*Set*` ***中的一个值可能只出现一次****；在* `*Set*` *的收藏*中独一无二

# 如何创建集合

创建一个`*Set*`非常简单。我们简单地创建一个`*Set*`的`*new*`实例，如下所示:

```
let mySet = new Set();
```

简单吧？做一个没有值的`*Set*`其实没什么意义。您可以使用几种不同的方法轻松地将值添加到`*Set*`中。要么通过添加一个`*iterable*`对象作为参数，要么通过使用位于`*Sets*`原型上的`*add()*`方法。

```
//Adding data from array
let mySet = new Set(someArray)//Add two simple values
let mySet = new Set();
mySet.add(‘Donatello’).add(‘Leonardo’);
```

一个`*Set*`只能存储唯一的值，这意味着如果你将“ ***莱昂纳多*** ”添加两次，它将只为“ ***莱昂纳多*** ”保存一个值。

集合包含其他方法，如

*   有()
*   大小()
*   删除()
*   大小()
*   等等

您可以通过查看文档了解更多信息:
[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Set # Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set#Methods)

允许您创建唯一值的集合，那么这实际上意味着什么呢？基本上，这意味着对`*Set*`中的值进行相等性测试，就像使用= = =(JavaScript 中的相等运算符)一样。

```
100 === 100 // true  
'Leonardo' === ''Leonardo' // true
100 === ‘100’ // false
```

# 寻找特定元素

为了检查一个元素是否存在于一个`*Set*`中，我们必须使用`*has()*`方法。这将返回一个真/假值，很像`*array.prototype.includes()*`方法。

```
console.log(mySet.has(1)); //true
console.log(myArray.includes(1)); //true
console.log(myArray.indexOf(1)); //0
```

但是，与数组不同，集合不支持获取特定值，因此如果您尝试:

```
console.log(mySet[0]); //undefined
console.log(myArray[0]); //1
```

> **我个人觉得 Set.has()比 array.indexOf()更容易使用
> 还要注意，如果你发现自己在使用 array.includes()，它在 Internet Explorer 中不受支持**

# 获取集合的大小

当我们有一个唯一的`*Set*`时，我们经常需要获得一个大小的大小，就像处理数组时使用`*array.length*`一样。

`*Set*`持有一个可以让我们非常容易得到尺寸的方法，叫做 size()……(Go figure；) )

size 方法返回一个`*Set*`对象中元素的数量。

```
const number_of_different_companies = new Set(arrayOfData.map(item => item.getCompany().id)).size; // Will return a number, ex: 10
```

# 过滤掉数组中的重复项

使用`*Sets*`时，有可能通过一个`*array*`。这将从数组中创建一组唯一的值，这意味着它将从数组中删除任何重复的值。

让我们仔细看看。

```
// Create array
const myArray = ['**Splinter**', 'Rafael', 'Donatello', 'Michelangelo', 'Shredder', '**Splinter**'];//Convert to unique set of values
const myUniqueSet = new Set(myArray); // returns: "Splinter", "Rafael", "Donatello", "Michelangelo", "Shredder"

// Convert back to array
const myUniqueArray = [...myUniqueSet]; //returns "Splinter", "Rafael", "Donatello", "Michelangelo", "Shredder"
```

我们要做的第一件事是用我们的值创建一个数组，然后将它传递给一个集合，这将删除数组中所有重复的值(数组中有两次的分段值)。

我们正在做的最后一件事是将它转换回一个数组。主要原因是`*Sets*`不支持数组方法，比如:

*   `*array.map()*`
*   `*array.reduce()*`
*   `*array.filter()*`
*   等等

> **请注意，当您处理对象时可能会很棘手，因为只有当集合测试的对象具有相同的对象引用时，等式才会返回 true。**
> 
> 我个人也遇到过这样的问题，我有两个看起来相同的对象，但被认为是不相等的，因为它们有不同的对象引用。

在本文中了解更多关于对象引用的信息:[https://code burst . io/explaining-value-vs-reference-in-JavaScript-647 a 975 E12 a 0](https://codeburst.io/explaining-value-vs-reference-in-javascript-647a975e12a0)

# 循环集

然而，集合在其原型上包含一个`*forEach*`方法，这意味着我们可以循环集合中的所有值，而不必将其转换回数组。
也可以使用`*for of*` …循环来循环所有值

```
//ForEach
myUniqueSet.forEach(value => console.log(value)); // Logs each value 

 //For of
 for (let value of myUniqueSet) {
     console.log(value) // Logs each value
 }
```

你可以在这里了解更多关于你使用的可用方法:[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Set # Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set#Methods)

# 布景很快，非常快。

如果您已经在 JavaScript 领域工作了一段时间，并且以前处理过数据，那么您可能也在某个时候遇到过数组。
在数组中，我们可以添加/删除数据，查找特定元素等。

*   `*array.push()*`
*   `*array.splice()*`
*   `*array.indexOf()*`

通过使用一些可用的原型方法，您可以对集合做同样的事情。

在这里，您可以找到如下方法:

*   `*set.add()*`
*   `*set.remove()*`
*   `*array.has()*`

你可以在这篇文章中了解更多:[https://alligator.io/js/sets-introduction](https://alligator.io/js/sets-introduction/)

在听说并阅读了`*Sets*`如何提高 JavaScript 应用程序的速度之后，我产生了自己做一些测试的兴趣。令我惊讶的是，`*Sets*`不仅仅是快，与数组相比，它们快得惊人。

如今，浏览器通常都非常快，解析和执行 JavaScript 代码也非常快，所以我们需要创建一个包含足够多项的数组，这将给我们带来一定的延迟，以便我们可以测量操作之间的性能。

我尝试在一个 50，000 个项目的`*array*`上比较上述方法。

为了测量性能，我们将使用浏览器自带的控制台，使用

*首先创建一个默认为 50.000 项的数组:*

***注意:注意 fill()只能在支持 ES6 的浏览器中工作。***

```
*const arraySize = 50000;let array = new Array(arraySize).fill(arraySize);console.log( array.length ); // 50000*
```

***比较 Array.push 和 Set.add()***

*让我们试着比较一下上面的方法，看看它们的表现如何。*

*在本例中，我们将 50001 添加到现有的`*array*`和`*Set*`中。

数组测试:**0.36181640625 毫秒**
设置测试:**0.010009765625 毫秒***

```
*//Add values
console.time( 'arrayTest' );
array.push( arraySize + 1 );
console.timeEnd( 'arrayTest' );let set = new Set( array );console.time( 'setTest' );
set.add( arraySize + 1 );
console.timeEnd( 'setTest' );console.log( "array length", array.length ); // 50001
console.log( "setsize", set.size ); // 500001*/*
```

*正如你所看到的，set 要快得多——实际上**比**快了 189%。*

***比较 Array.splice 和 Set.delete()***

*让我们试着从数组和集合中删除 40，000 个项目，看看它们的性能如何比较:*

*array delete:**0.147216796875 毫秒**
set delete:**0.011962890625 毫秒***

```
*/Delete values
let deleteFromArray = ( arr, item ) => {
    var i = array.indexOf( item );
    i !== -1 && array.splice( i, 1 );
};console.time( 'arrayDelete' );
deleteFromArray( array, 40000 );
console.timeEnd( 'arrayDelete' );let set = new Set( array );console.time( 'setDelete' );
set.delete( 40000 );
console.timeEnd( 'setDelete' );*
```

*再说一次，电视节目的表现要好得多。这次**好了 169%**。*

***找到收藏中的特定物品***

*让我们试着找到一个特定的项目——我们可以通过使用`*array.indexOf()*`和`*set.has()*`来完成*

*array find:**0.1728515625 毫秒**
set find:**0.0859375 毫秒***

```
*// Helpers
let checkArr = ( array, item ) => array.indexOf( item ) !== -1;
let checkSet = ( set, item ) => set.has( item );// set variables
let set, result;console.time( 'arrayFind' );
result = checkArr( array, 40000 );
console.timeEnd( 'arrayFind' );set = new Set( array );console.time( 'setFind' );
checkSet( set, 40000 );
console.timeEnd( 'setFind' );*
```

*电视再次证明了自己的速度更快，性能提高了 67%。*

> *您的结果可能会显示一些其他数字。结果可能因设备、操作系统、浏览器等而异。*
> 
> *我在一台装有 Win10 和 Chrome73 的笔记本电脑上做了测试*
> 
> ***看看我在 Codepen 和 Fork 上的测试吧，如果你喜欢自己做测试的话:**[**https://codepen.io/NickyCDK/pen/bJOWBj**](https://codepen.io/NickyCDK/pen/bJOWBj)*

# *最后的想法*

*我不是使用`*Sets*`的专家，但是在我看过之后，它们看起来很棒。*

*看起来`*Sets*`通常比数组表现得更好。这是不是意味着你不应该再使用数组了？我会说不。它不是数组的替代品，因为数组可以做很多集合不能做的事情，反之亦然。**例如，在集合中，你不能访问一个特定的索引，并获取那个索引的值。***

*最大的区别是`*arrays*`可以保存值的副本而`*Sets*`不能**(无论你做什么)**。另外，数组是索引集合，集合是键控集合。

性能的提升让我感到惊讶，就我个人而言，我可能会更频繁地使用`*Set*`，因为与数组相比，它们在定位元素和添加/删除元素时表现得更好。*

*同样，如果你记得…在集合中我们不能使用数组方法。然而，这可以通过将`*Set*`转换回`*array*`来解决:*

```
*// Example on convert set to an array and using the array.map() method.
let myArray = […mySetOfNames].map(name => {firstname: name.firstname});*
```

*当您将集合转换回数组时，所有数组方法都可以再次使用，因为它现在是一个数组。*

*总的来说，在我看来，这两者的结合似乎是一种依赖于场景的方式，但我很想听听你的意见，你会如何使用它，你用它来做什么？*

*感谢阅读，我希望你喜欢这篇文章，如果是的话，请点击按钮或订阅来支持我。*

*如果你还不是中等会员，考虑成为一名吧！你可以接触到很棒的内容，并有机会与他人分享你自己的知识。在这里注册每月只需 5 美元。*

*[](/typescript-interfaces-explained-in-2-minutes-af1637b88bd4) [## 两分钟解释的类型脚本接口

### 在这篇小文章中，您将学习什么是接口，以及如何在您自己的项目中创建和使用接口。

javascript.plainenglish.io](/typescript-interfaces-explained-in-2-minutes-af1637b88bd4) [](/typescript-generics-explained-in-2-minutes-c95e49783347) [## 用 2 分钟的时间用例子解释了类型脚本泛型

### 深入探究类型脚本泛型

javascript.plainenglish.io](/typescript-generics-explained-in-2-minutes-c95e49783347) [](https://medium.com/js-dojo/vuejs-tips-best-practices-39d9962bb255) [## VueJS —技巧和最佳实践

### 在构建 Vue 应用时，你应该做什么，应该避免什么，通常只是一些简单的好建议

medium.com](https://medium.com/js-dojo/vuejs-tips-best-practices-39d9962bb255) [](https://medium.com/js-dojo/build-a-website-using-nuxt-contentful-a-step-by-step-guide-b75217ccdfa) [## 使用 Nuxt & Contentful 建立网站——一步一步的指南

### 了解如何使用 Vue/NuxtJS 构建一个简单的网站 Contentful——还包括一个 Vuex 示例。

medium.com](https://medium.com/js-dojo/build-a-website-using-nuxt-contentful-a-step-by-step-guide-b75217ccdfa) [](https://medium.com/front-end-weekly/a-closer-look-on-array-reduce-with-useful-examples-34f222664e66) [## 通过有用的示例进一步了解 array.reduce()

### 提高您的 javascript 技能，并通过一些有用的示例学习如何使用 Array.prototype.reduce()

medium.com](https://medium.com/front-end-weekly/a-closer-look-on-array-reduce-with-useful-examples-34f222664e66) 

***如果你想找个时间和我聊聊，请关注我的***[***Twitter***](https://twitter.com/nickycdk)***|***[***LinkedIn***](https://www.linkedin.com/in/dknickychristensen/)***或者直接访问我的*** [***网站***](https://nickychristensen.dk/) ***(不过是丹麦文)***

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。**