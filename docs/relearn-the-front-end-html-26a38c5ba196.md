# 重新学习前端— HTML

> 原文：<https://javascript.plainenglish.io/relearn-the-front-end-html-26a38c5ba196?source=collection_archive---------2----------------------->

## 作为初级前端工程师探索您的学习路径，或者作为高级前端工程师复习您的知识。

![](img/c3bd0679b0c635a548977c7d63a10ed0.png)

Photo by [Jackson Sophat](https://unsplash.com/@jacksonsophat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我会花一个月的时间整理前端相关的知识。一方面我会巩固自己的技能。另一方面，我会用它来分享初级前端工程师的学习路径和高级前端工程师的知识复习。

总体文章目录

*   [重新学习前端— HTML](/relearn-the-front-end-html-26a38c5ba196)
*   [重新学习前端——CSS](/relearn-the-front-end-css-4d74eb5981f8)
*   [重新学习前端— JavaScript 基础知识](/relearn-the-front-end-javascript-basics-d770eefd791f)
*   [重新学习前端——面向 JavaScript 对象](/relearning-the-front-end-javascript-object-oriented-913077e735bf)
*   [重新学习前端— JavaScript V8 引擎机制](/relearning-the-front-end-javascript-v8-engine-mechanism-cc6457b43aff)
*   [重新学习前端—浏览器渲染机制](/relearning-the-front-end-browser-rendering-mechanism-efbfc19d225f)
*   [重新学习前端—浏览器缓存策略](/relearn-the-front-end-browser-caching-strategy-21cd081886d)
*   [重新学习前端—排序算法](/relearn-the-front-end-sorting-algorithm-348f939632e0)
*   [重新学习前端—设计模式](/relearning-the-front-end-design-patterns-e95444b6bdb)
*   [重新学习前端网络](/relearn-the-front-end-network-b0402a870336)
*   [重新学习前端—前端安全](/relearning-the-front-end-front-end-security-bbc20ded6b12)

这篇文章是关于 HTML 的

# 1 谈论 HTML5 在标签、属性、存储和 API 方面的新特性

*   **标签**:添加语义标签(`aside/figure/section/header/footer/nav`)，添加多媒体标签视频和音频，使风格和结构更加分离
*   **属性**:增强表单，主要是增强输入的 type 属性，给 meta 添加 charset 设置字符集，给 script 添加 async 异步加载脚本
*   **存储**:增加`localStorage, sessionStorage, and indexedDB`，引入应用缓存，缓存 web 和应用
*   **API** :添加拖拽 API、地理定位、SVG 绘图、画布绘图、Web Worker、WebSocket

# 2 doctype 的作用是什么？

声明文档类型，告诉浏览器使用什么文档标准来解析该文档:

*   **怪异模式**:浏览器使用其模式解析文档，默认为怪异模式，不添加 doctype
*   **标准模式**:浏览器根据 W3C 标准解析文档

# 3 前端存储的几种类型以及它们之间的区别

*   **cookie**:html 5 之前本地存储的主要方法，大小只有 4k，HTTP 请求头会自动带 cookie，兼容性好
*   **local storage**:html 5 的一个新特性，持久存储，即使页面关闭也不会被清除，以键值对的形式存储，大小为 5M
*   **SessionStorage**:html 5 中的一个新特性，操作和大小与 localStorage 相同，与 localStorage 的区别在于关闭一个标签页(页面)时 sessionStorage 被清除，不同标签页之间的 session storage 不可互操作
*   **IndexedDB** : NoSQL 数据库，类似于 MongoDB，使用键值对进行存储，异步操作数据库，支持事务，可以存储 250MB 以上的存储空间，但是 IndexedDB 受到同源策略的限制
*   **Web SQL** :是在浏览器上模拟的关系数据库。开发者可以通过 SQL 语句操作 Web SQL。是 HTML5 之外的一套独立规范，兼容性差。

# href 和 src 有什么区别

`href` (hyper reference):浏览器遇到 href 时，会并行下载资源，不会阻塞页面解析。比如我们用`<link>`导入 CSS，浏览器会并行下载 CSS，不会阻塞页面解析。所以我们建议在导入 CSS 时使用`<link>`而不是`@import`

```
<link href=”style.css” rel=”stylesheet” />
```

复制代码`src`(资源)。当浏览器遇到 src 时，会暂停页面解析，直到资源被下载或执行，这也是脚本标签放在底部的原因。

```
<script src=”script.js”></script>
```

# 5 meta 的属性是什么，作用是什么？

meta 标签用于描述网页的元信息，如网站`author`、`description`、`keywords`。元以`name=xxx`和`content=xxx`的形式定义信息。常用的设置如下:

**字符集**:定义 HTML 文档的字符集

```
<meta charset=”UTF-8" >
```

**http-equiv** :可以用来模拟 http 请求头，可以设置过期时间，缓存，刷新

```
<meta http-equiv=”expires” content=”Wed, 20 Jun 2019 22:33:00 GMT”>
```

**视窗**:用于控制页面宽度、高度和缩放比例

```
<meta
 name=”viewport”
 content=”width=device-width, initial-scale=1, maximum-scale=1"
>
```

# 6 视口的参数是什么，它们的作用是什么？

*   **宽度/高度**:宽度和高度，默认宽度 980px
*   **初始比例**:初始比例，1~10
*   **最大/最小比例**:允许用户缩放的最大/最小比例
*   **用户可扩展**:用户是否可扩展(是/否)

# 7 http-equiv 属性的角色和参数

*   **到期**:指定到期时间
*   **杂注**:设置 no-cache 以禁用缓存
*   **刷新**:定期刷新
*   **设置 cookie** :可以设置 cookie
*   **X-UA 兼容**:使用浏览器版本
*   **apple-mobile-we b-app-status-bar-style**:对于 WebApp 全屏模式，隐藏状态栏/设置状态栏颜色

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----26a38c5ba196--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----26a38c5ba196--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----26a38c5ba196--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----26a38c5ba196--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----26a38c5ba196--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----26a38c5ba196--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***