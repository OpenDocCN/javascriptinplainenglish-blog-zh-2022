# 重新学习前端— JavaScript 基础知识

> 原文：<https://javascript.plainenglish.io/relearn-the-front-end-javascript-basics-d770eefd791f?source=collection_archive---------4----------------------->

## 作为初级前端工程师探索您的学习路径，或者作为高级前端工程师复习您的知识。

![](img/d26d693f12329506978736fe2df9a198.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我会花一个月的时间整理前端相关的知识。一方面我会巩固自己的技能。另一方面，我会用它来分享初级前端工程师的学习路径和高级前端工程师的知识复习。

总体文章目录

*   [重新学习前端— HTML](/relearn-the-front-end-html-26a38c5ba196)
*   [重新学习前端——CSS](/relearn-the-front-end-css-4d74eb5981f8)
*   [重新学习前端——JavaScript 基础知识](/relearn-the-front-end-javascript-basics-d770eefd791f)
*   [重新学习前端——面向 JavaScript 对象](/relearning-the-front-end-javascript-object-oriented-913077e735bf)
*   [重新学习前端— JavaScript V8 引擎机制](/relearning-the-front-end-javascript-v8-engine-mechanism-cc6457b43aff)
*   [重新学习前端—浏览器渲染机制](/relearning-the-front-end-browser-rendering-mechanism-efbfc19d225f)
*   [重新学习前端—浏览器缓存策略](/relearn-the-front-end-browser-caching-strategy-21cd081886d)
*   [重新学习前端—排序算法](/relearn-the-front-end-sorting-algorithm-348f939632e0)
*   [重新学习前端—设计模式](/relearning-the-front-end-design-patterns-e95444b6bdb)
*   [重新学习前端网络](/relearn-the-front-end-network-b0402a870336)
*   [重新学习前端—前端安全](/relearning-the-front-end-front-end-security-bbc20ded6b12)

这篇文章是关于 JavaScript 基础知识的

# 1 手写一个防抖功能

防抖，即短时间内同一事件的大量触发只会执行一次功能。实现原理是设置一个定时器，约定 xx 毫秒后触发事件处理。每次事件被触发时，定时器将被重置，直到 xx 毫秒。没有二次操作，防抖常用于搜索框/滚动条的监控事件处理。如果不执行防抖，每次输入单词或滚动屏幕都会触发事件处理，导致性能浪费。

# 2 手动编写一个节流函数

防抖是延迟执行，节流是间隔执行。函数节流每隔一段时间执行一次。实现原理是设置一个定时器，约定 xx 毫秒后执行事件。如果时间到了，执行该功能并复位。定时器和防抖的区别在于，防抖在每次触发事件时都会重置定时器，而节流则是在定时器到期后清除定时器。

**实现 2** :使用两个时间戳 prev old timestamp 和 now new timestamp，每次触发事件时判断两者的时间差。如果达到了指定的时间，执行该函数并重置旧的时间戳

# 3 如何在 ES5 环境中实现 let

这个问题对于回答 let 和 var 的区别至关重要。对于这个问题，我们可以直接查看巴别塔转换前后的结果，看看 let 在循环中定义的变量是如何解决变量提升问题的

Babel 为 let 定义的变量添加了一个下划线，以避免访问块级范围之外的变量。除了变量名的转换，我们还可以通过自执行函数模拟块级作用域。

但是这个问题并没有结束，我们再回到 var 和 let/const 的区别:

*   var 声明的变量会挂在窗口上，而`let`和`const`不会
*   var 声明的变量有变量提升，而`let`和`const`没有
*   `Let`和`const`声明形成一个块范围，只能在块范围内访问，不能跨块或函数访问
*   `Let`和`const`不能在同一个作用域内声明同名的变量，但是 var 可以
*   临时死区，用`let`和`const`声明的变量不能在声明前使用

巴别塔的转化只达到第 2，3，5 点

# 4 如何在 ES5 环境中实现 const

实现 const 的关键在于`Object.defineProperty() API`，它用于添加或修改对象的属性。通过配置属性描述符，您可以精确地控制属性`behavior. Object.defineProperty()`接受三个参数:

```
Object.defineProperty(obj, prop, desc)
```

对于常量不可修改的特性，我们通过设置 writable 属性来实现

# 5 手写通话()

`call()`方法使用指定的 this 值和一个或多个单独给出的参数调用函数

```
Syntax: function.call(thisArg, arg1, arg2, …)
```

`call()`的原理比较简单。因为函数的 this 指向它的直接调用者，我们改变调用者来完成 this 指向的改变:

基于以上原则，我们可以用两行代码实现`call()`

但是我们还有一些细节需要改进:

# 6 手写申请()

`apply()`方法用给定的这个值调用一个函数，参数以数组(或类似数组的对象)的形式提供。

```
Syntax: func.apply(thisArg, [argsArray])
```

`apply()`类似于`call()`，不同的是`call()`接受的是一个参数表，而`apply()`接受的是一个参数数组，所以我们可以简单的在`call()`的实现中改变输入参数的形式

# 7 手写装订()

`bind()`方法创建了一个新函数。调用`bind()`时，新函数的 this 被指定为`bind()`的第一个参数，其余参数将作为新函数的参数，在调用时使用。

```
Syntax: function.bind(thisArg, arg1, arg2, …)
```

从用法上看，好像给`call/apply`包装一层功能就实现了`bind()`:

但是我们忽略了三点:

*   除此之外，`bind()`还接受其他参数。`bind()`返回的函数也接受参数。这两部分参数都必须传递给返回的函数。
*   New 将改变 this point:如果绑定函数是新的，那么 this point 将改变，指向当前函数的实例
*   原型链上的原始函数的属性和方法不会被保留

# 8 数组展平

> 对于像[1，[1，2]，[1，2，3]]这样的多级嵌套数组，怎么才能像[1，1，2，1，2，3]一样展平成一维呢数组:

## 8.1 迭代+扩展运算符

```
let arr = [1, [1,2], [1,2,3,[4,4,4]]]
while (arr.some(Array.isArray)) {
  arr = [].concat(...arr);
}console.log(arr)  // [1, 1, 2, 1, 2, 3, 4, 4, 4]
```

## 8.2 ES6 平板()

```
const arr = [1, [1,2], [1,2,3]]
arr.flat(Infinity)  // [1, 1, 2, 1, 2, 3]
```

## 8.3 序列化后的正规化

```
const arr = [1, [1,2], [1,2,3]]
const str = `[${JSON.stringify(arr).replace(/(\[|\])/g, '')}]`
JSON.parse(str)   // [1, 1, 2, 1, 2, 3]
```

## 8.4 递归

对于树形结构的数据，最直接的处理方法是递归

```
const arr = [1, [1,2], [1,2,3]]
function flat(arr) {
  let result = []
  for (const item of arr) {
    item instanceof Array ? result = result.concat(flat(item)) : result.push(item)
  }
  return result
}flat(arr) // [1, 1, 2, 1, 2, 3]
```

## 8.5 reduce()递归

```
const arr = [1, [1,2], [1,2,3]]
function flat(arr) {
  return arr.reduce((prev, cur) => {
    return prev.concat(cur instanceof Array ? flat(cur) : cur)
  }, [])
}flat(arr)  // [1, 1, 2, 1, 2, 3]
```

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----d770eefd791f--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----d770eefd791f--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----d770eefd791f--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----d770eefd791f--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----d770eefd791f--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----d770eefd791f--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***