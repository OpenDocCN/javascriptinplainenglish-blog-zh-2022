# 重新学习前端— CSS

> 原文：<https://javascript.plainenglish.io/relearn-the-front-end-css-4d74eb5981f8?source=collection_archive---------7----------------------->

## 作为一名初级前端开发人员探索您的学习路径，或者作为一名高级前端工程师回顾您的知识。

![](img/3c9e6158e658400d9b263ce95e7c674e.png)

Photo by [Jackson Sophat](https://unsplash.com/@jacksonsophat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我会花一个月的时间整理前端相关的知识。一方面，我会巩固我的技能。另一方面，我会用它来分享初级前端工程师的学习路径和高级前端工程师的知识复习。

整体文章目录:

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

这篇文章是关于 CSS 的

# 1.清除浮动的方法

为什么要清除浮动:清除浮动是为了解决父元素的高度因子元素浮动而塌陷的问题

## 1.1.添加新元素

## 1.2.使用伪元素

## 1.3.触发父元素 BFC

# 2.灵活布局

> 容器属性(用于 flex 布局容器的属性)

## **调整-内容**

定义子元素在主轴(水平轴)上的对齐方式

```
.container {
    justify-content: center | flex-start | flex-end | space-between | space-around;
}
```

## 对齐-项目

定义已定义项目在横轴(纵轴)上的对齐方式

```
.container {
    align-items: center | flex-start | flex-end | baseline | stretch;
}
```

## 弯曲方向

主轴(水平轴)方向

```
.container {
    flex-direction: row | row-reverse | column | column-reverse;
}
```

## 柔性包装

新行

```
.container {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

## 柔性流

`flex-flow`属性是伸缩方向属性和`flex-wrap`的简写

```
.container {
    flex-flow: <flex-direction> || <flex-wrap>;
}
```

## 对齐内容

定义多条网格线的对齐方式

```
.container {
    align-content: center | flex-start | flex-end | space-between | space-around | stretch;
}
```

项目属性(用于容器中子元素的属性)

## 灵活增长

**定义项目的放大倍率，默认为 0，即使有剩余空间也不会放大**。如果所有的子元素 flex-grow 都是 1，那么剩余空间将被平均分配，如果一个子元素`flex-grow`是 2，那么这个子元素将占据 2 倍的剩余空间

```
.item {
    flex-grow: <number>; /* default 0 */
}
```

## 弯曲收缩

定义该项的缩小比例，默认为 1，即如果没有足够的空间，子元素将被缩小。如果所有子元素`flex-shrink`都是 1，并且一个子元素`flex-shrink`是 0，那么这个子元素不会收缩

```
.item {
    flex-shrink: <number>; /* default 1 */
}
```

## 弹性基础

在分配额外空间之前，定义项目占用的主轴空间。默认值是 auto，这是子元素的原始大小。如果设置为固定值，子元素将占用固定的空间。

```
.item {
    flex-basis: <length> | auto; /* default auto */
}
```

## 弯曲

flex 属性是`flex-grow, flex-shrink and flex-basis`的简写。默认值为 0 1 auto，即剩余空间不会被扩大。如果剩余空间不够，就会减少，子元素占用它的大小。

```
.item {
    flex: none | [ <’flex-grow’> <’flex-shrink’>? || <’flex-basis’> ]
}
```

Flex 有两个快捷方式值:auto 和 none，分别代表`1 1 auto`(如果有剩余空间，会平均分配，如果空间不够，会按比例减少，子元素占用的空间等于其大小)和`0 0 auto`(有剩余空间，不会分配。空间不够且不收缩，子元素占用的空间等于其大小)

## 命令

定义项目的排序顺序。值越小，排名越高，默认为 0

```
.item {
    order: <integer>;
}
```

## 自我对齐

定义单个子元素的排列。例如，align-items 将中心设置为将所有子元素居中对齐。然后，您可以通过将 align-self 设置为子元素来单独设置子元素的顺序。

```
.item {
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

# 3.什么是 BFC

BFC 的全称是**块格式化上下文**，即块级格式化上下文。简单来说，BFC 就是页面上一个孤立独立的容器，不受外界干扰或外界干扰。

## 3.1.如何触发 BFC

*   `Float`不是没有
*   `overflow`的值不可见
*   `position`是绝对的还是固定的
*   `display`的值是内嵌块或表格单元格或表格标题或网格

## 3.2.BFC 的渲染规则是什么

*   BFC 在页面上是一个孤立的独立容器，不受外界干扰或外界干扰
*   计算 BFC 高度时，浮动子元素也参与计算(即内部有浮动元素时不会发生高度折叠)
*   BFC 的区域不会与浮动的元素区域重叠
*   BFC 内的元素垂直放置
*   BFC 中两个相邻元素的边距会重叠

## 3.3.BFC 的应用场景

*   **清除浮动**:BFC 内部的浮动元素会参与高度计算，可以用来清除浮动，防止高度崩溃
*   **避免一个元素被浮动元素覆盖**:BFC 的区域不会与浮动元素的区域重叠
*   **防止页边距重叠**:属于同一个 BFC 的两个相邻方框的页边距会折叠，但不同的 bfc 不会折叠

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----4d74eb5981f8--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----4d74eb5981f8--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----4d74eb5981f8--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----4d74eb5981f8--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----4d74eb5981f8--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----4d74eb5981f8--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***