# 重新学习前端:JavaScript V8 引擎机制

> 原文：<https://javascript.plainenglish.io/relearning-the-front-end-javascript-v8-engine-mechanism-cc6457b43aff?source=collection_archive---------2----------------------->

![](img/4569366773dedd624b0d104542dbaf8f.png)

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

这篇文章是关于 JavaScript V8 引擎机制的。

# 1 如何在 V8 中执行一段 JS 代码

*   **预分析**:检查语法错误，但不生成 AST
*   **生成 AST** :经过词法/语法分析，生成抽象语法树
*   **生成字节码**:基线编译器(点火)将 AST 转换成字节码
*   **生成机器码**:优化编译器(涡扇)将字节码转换成优化的机器码。另外，在逐行执行字节码的过程中，如果经常执行一段代码，V8 会直接将这段代码转换保存为机器码，下一次执行不需要经过字节码，优化了执行速度

# 2 引用计数和标记清理简介

*   **引用计数**:如果一个变量被赋予了引用类型，那么该对象的引用数为+1。如果变量变成另一个值，那么对象的引用数是-1，垃圾收集器将回收引用数为 0 的对象。但是，当对象被循环引用时，引用的次数永远不会归零，导致无法释放内存。
*   **标记移除**:垃圾收集器先标记内存中的所有对象，然后从根节点开始遍历，移除被引用对象和运行环境中对象的标记，剩下的标记对象不可访问，等待回收对象。

# V8 如何执行垃圾收集

JS 引擎中变量有两个主要的存储位置，堆栈内存和堆内存。堆栈内存存储基本类型数据和引用类型数据的内存地址，堆内存存储引用类型数据。

**栈内存回收**:调用栈上下文切换后，栈内存被回收，比较简单

**堆内存回收** : V8 的堆内存分为新一代内存和老一代内存。新一代内存是临时分配的内存，存在时间短，而老一代内存存在时间长。

## 新一代内存回收机制

新一代的内存容量很小，在 64 位系统下只有 32M。新生代的记忆分为两部分:从和到。执行垃圾回收时，首先扫描 From，恢复非存活对象，存活对象按顺序复制到 to，然后交换 From/To，等待下一次恢复

## 老一代内存回收机制

*   **提升**:如果多次采集后年轻一代的变量仍然存在，则放入老一代的记忆中
*   **标记移除**:老一代内存会先遍历所有对象并进行标记，然后取消正在使用或强引用的对象的标记，并回收已标记的对象
*   **整理内存碎片**:将对象移动到内存的一端

# 4.JS 为什么比 C++等语言慢，V8 做了哪些优化？

## 4.1 的问题

*   **动态类型**:每次访问属性/seek 方法，都需要先检查类型；此外，动态类型很难在编译阶段进行优化
*   **属性访问**:在 C++/Java 等语言中，方法、属性存储在数组中，只能通过数组移位来获取，而 JS 存储在对象中，每次获取都要进行哈希查询。

## 4.2 针对 V8 的优化

*   **优化 JIT**(just-in-time compilation):与 C++/Java 等编译语言相比，JS 是一边解释一边执行，效率较低。V8 对这个过程进行了优化:如果一段代码执行了多次，V8 会将这段代码转换成机器码并缓存，下次运行时直接使用机器码。
*   **隐藏类**:对于 C++等语言，只需要很少的指令就可以通过 offset 获取变量信息，而 JS 需要进行字符串匹配，效率很低。V8 借用类和偏移位置的思想将对象划分成不同的组，即隐藏类。
*   **嵌入式缓存**:即缓存对象查询的结果。一般的查询过程是:获取隐藏类地址- >根据属性名查找偏移值- >计算属性地址，嵌入式缓存就是这个过程结果的缓存。

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----cc6457b43aff--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----cc6457b43aff--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----cc6457b43aff--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----cc6457b43aff--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----cc6457b43aff--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----cc6457b43aff--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****