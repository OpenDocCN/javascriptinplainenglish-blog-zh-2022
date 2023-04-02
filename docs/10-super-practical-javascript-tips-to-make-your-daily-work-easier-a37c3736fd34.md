# 10 个超级实用的 JavaScript 技巧，让你的日常工作更简单

> 原文：<https://javascript.plainenglish.io/10-super-practical-javascript-tips-to-make-your-daily-work-easier-a37c3736fd34?source=collection_archive---------8----------------------->

## **作为一名前端开发工程师，这十项开发技能是必须掌握的；否则，我们的工作会比需要的更困难。**

![](img/aae2470241ac48e45dd04b715c160943.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**让我们来看看这 10 个实用小技巧是什么:**

**1。过滤错误值**

如果要过滤数组中的 false、0、null、undefined 等值，可以这样做:

```
const array = [1, 0, undefined, 6, 7, ‘’, false]; array.filter(Boolean);
```

**2。判断简化**

如果有这样的判断:

```
if(a === undefined || a === 10 || a=== 15 || a === null) { //… } 
```

您可以使用数组来简化这种判断逻辑:

```
if([undefined, 10, 15, null].includes(a)) { //… }
```

这样代码会简单很多，也更容易扩展。如果还有一个判断需要等于 a，可以直接加到数组里。

**3。初始化数组**

您需要初始化一个指定长度的一维数组，并指定一个默认值，可以这样做:

```
const array = Array(6).fill(‘’); // [‘’, ‘’, ‘’, ‘’, ‘’, ‘’]
```

如果需要初始化具有指定长度的二维数组并指定默认值，可以这样做:

```
const matrix = Array(6).fill(0).map(() => Array(5).fill(0));
```

**4。清除数组**

要清除数组，请将数组的长度设置为 0:

```
let array = [“A”, “B”, “C”, “D”, “E”, “F”] array.length = 0 console.log(array) // []
```

**5。连接数组**

我们需要连接几个数组，我们可以使用 spread 运算符:

```
const start = [1, 2] const end = [5, 6, 7] const numbers = [9, …start, …end, 8] // [9, 1, 2, 5, 6, 7 , 8]
```

或者使用数组的`concat()`方法:

```
const start = [1, 2, 3, 4] const end = [5, 6, 7] start. concat(end); // [1, 2, 3, 4, 5, 6, 7]
```

但是当使用`concat()`方法时，如果要合并的数组很大，`concat()`函数在创建一个单独的新数组时会消耗大量内存。此时，您可以使用以下方法来合并阵列:

```
Array.prototype.push.apply(start, end)
```

通过这种方式，内存使用大大减少。

6。将数组元素转换成数字

如果有一个数组，并且需要将数组中的元素转换为数字，可以使用 map 方法来实现这一点:

```
const array = [‘12’, ‘1’, ‘3.1415’, ‘-10.01’]; array.map(Number); // [12, 1, 3.1415, -10.01]
```

这样，map 将在遍历数组时对数组的每个元素执行 Number 构造函数，并返回结果。

7。将类数组转换为数组

可以使用以下方法将类似数组的参数转换为数组:

```
Array.prototype.slice.call(arguments);
```

除此之外，还可以使用 spread 运算符来实现:
`[…arguments]`

8。Shorten console.log()

每次调试时都要编写大量的 console.log()可能很麻烦，您可以使用下面的形式来简化这段代码:

```
const c = console.log.bind(document) c(321) c(“hello mygod”)
```

每次执行 c 方法时都会这样做。

9。删除一个数组元素

如果我们想删除数组中的一个元素，可以使用 delete 来实现，但是删除后的元素会变得未定义，不会消失，而且在执行时会消耗大量的时间，这在大多数情况下无法满足我们的需求。因此，您可以使用数组的 splice()方法来移除数组元素:

```
const array = [“a”, “b”, “c”, “d”] array.splice(0, 2) // [“a”, “b”]
```

10。检查对象是否为空

我们需要检查对象是否为空，我们可以使用下面的:

```
Object.keys({}).length // 0
Object.keys({key: 1}).length // 1 
```

`Object.keys()`方法用于获取对象的键，并返回包含这些键值的数组。如果返回的数组长度为 0，则对象必须为空。

**感谢您的阅读，期待您的关注。**

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****