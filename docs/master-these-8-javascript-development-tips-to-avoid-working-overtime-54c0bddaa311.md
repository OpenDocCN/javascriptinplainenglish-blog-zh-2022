# 掌握这 8 个 JavaScript 开发技巧，避免加班

> 原文：<https://javascript.plainenglish.io/master-these-8-javascript-development-tips-to-avoid-working-overtime-54c0bddaa311?source=collection_archive---------8----------------------->

## 为了避免过度工作，您应该牢记的重要 JavaScript 开发技巧。

![](img/8229fa9a4fec1d86321c04f31ddd235d.png)

Photo by [freestocks](https://unsplash.com/@freestocks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

【JavaScript 开发技术有很多，那么哪些技术可以减轻我们的负担呢？大家一起讨论一下吧。下面这些技巧，真的在普通项目中帮了不少忙，缓解了不少压力。

1.  **用哪种方法删除数组元素**
    在项目中，经常需要删除数组中的一个元素。可能我们首先想到的是用 delete 来实现，但是大家都知道删除后的元素会变得不明确，不会完全消失，执行时会消耗大量的时间，所以实际上这并不符合我们的需求，也不是最优解。所以在这里，我们可以使用数组的 splice()方法来删除数组元素:

```
const array = ["b", "c", "d", "e"]array.splice(0, 2) // ["b", "c"]
```

**2。如何检查对象是否为空**
我们经常会遇到需要检查对象是否为空的情况。对于这个需求，有一个比较简单方便的方法，那就是使用 Object.keys()方法获取对象的 key，它会返回一个包含这些 key 的值。数组。如果返回的数组长度为 0，则对象必须为空。这个方法是不是很巧妙，我们来看看:

```
Object.keys({}).length  // 0Object.keys({key: 1}).length  // 1
```

**3。尽可能避免使用 eval()和 with()**
为什么要尽可能避免使用 eval()和 with()。让我们来看看使用这些的问题

(1) with()将在全局范围内插入一个变量。因此，如果另一个变量具有相同的名称，可能会导致混淆并覆盖该值。
(2)对于 eval()，应该是一个比较耗费资源的操作，因为每次调用，脚本引擎都要将源代码转换成可执行代码。

![](img/8127c9b974438b45b7f467608eeb59ce.png)

Photo by [Possessed Photography](https://unsplash.com/@possessedphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**4。缩短 console.log()**
调试的时候每次都要写很多 console.log()是很麻烦的，所以我们可以用下面的形式来简化这段代码，下面的方法每次都足以执行 c 方法。

```
const c = console.log.bind(document)
```

**5。如何过滤错误值**
对于项目需求，我们经常会在数组中遇到 false、0、null、undefined 等需要过滤的值，这时我们可以使用以下方法:

```
const array = [3, 4, undefined, 8, 9, '', false];array.filter(Boolean);// [3, 8, 9]
```

![](img/a8d0831a820bf1df2e6325c25f2a6bfc.png)

Photo by [Tyler Nix](https://unsplash.com/@nixcreative?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**6。使用 map()对数组元素进行统一操作**
首先我们来看看 map()的方法是什么:创建一个新的数组，由原数组中每个元素被调用一次所提供的函数的返回值组成。
为了简单明了，我们举个例子来说明:对数组中的所有元素执行*3 运算

```
let arr = [1,2,3]arr = arr.map(item=>item*2)console.log(arr);   //[ 1,6,9 ]
```

**7。使用 Array.from()将 Array-like 转换为 array**
如上，我们先来了解一下 Array.from()方法是什么:创建一个 array-like 或 iterable 对象的新的浅拷贝 array 实例。如果你觉得这个解释太负责，那么我们也可以这样理解:一个有长度，有几个指数的物体。

```
let str  = 'bcd'str = Array.from(str)console.log(str);   //   [ 'b', 'c', 'd' ]
```

![](img/7339de94e657a0ee743a85181fba00b9.png)

Photo by [Jeremy Bezanger](https://unsplash.com/@unarchive?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**8。如何最快最简单的清除数组**T5 在项目中，我们经常会遇到需要清除一个数组，数组的长度可以设置为 0:

```
let array = ["b", "c", "d"]array.length = 0console.log(array)  // []
```

**感谢您的阅读，期待您的关注，让我们一起进步。**

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***