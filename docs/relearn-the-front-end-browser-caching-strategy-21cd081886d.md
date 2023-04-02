# 重新学习前端—浏览器缓存策略

> 原文：<https://javascript.plainenglish.io/relearn-the-front-end-browser-caching-strategy-21cd081886d?source=collection_archive---------6----------------------->

## 作为初级前端工程师探索您的学习路径，或者作为高级前端工程师复习您的知识。

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

这篇文章是关于浏览器缓存策略的。

# 1.介绍浏览器缓存位置和优先级

*   服务行业人员
*   超高速缓冲存储系统
*   磁盘高速缓存
*   推送缓存
*   如果未命中上述缓存，将发出网络请求

# 2.不同缓存之间的差异

## 2.1 服务人员

类似于 Web Worker，是一个独立的线程。我们可以在这个线程中缓存文件，在主线程需要的时候在这里读取文件。Service Worker 允许我们自由选择缓存哪些文件以及文件的匹配和读取规则。并且缓存是持久的。

## 2.2 内存缓存

也就是内存缓存，内存缓存不是持久的，缓存会随着进程的释放而释放。

## 2.3 磁盘缓存

也就是硬盘缓存。与内存缓存相比，硬盘缓存具有更好的持久性和容量。它会根据 HTTP 头的字段判断哪些资源需要缓存。

## 2.4 推送缓存

也就是推送缓存，也就是 HTTP/2 内容，目前用的比较少。

# 3.浏览器缓存策略

## **3.1 强缓存(不要向服务器要缓存)**

## 设置过期

也就是到期时间。例如，“Expires: Thu，2019 年 12 月 26 日 10:30:42 GMT”表示缓存将在此时间后过期。该截止日期是一个绝对日期。如果本地日期被修改，或者本地日期与服务器日期不一致，那么缓存过期时间将是错误的。

## 设置缓存控制

HTTP/1.1 新增了一个字段，`Cache-Control`可以通过 max-age 字段设置过期时间，比如`Cache-Control:max-age=3600`另外，Cache-Control 还可以设置 private/no-cache 等。一种领域。

## **3.2 协商缓存(需要询问服务器缓存是否过期)**

## 最后修改的

也就是最后一次修改时间。当浏览器第一次请求资源时，服务器会将 Last-Modified 添加到响应头中。当浏览器再次请求资源时，浏览器将把 If-Modified-Since 字段带到请求头中。该字段的值是由先前的服务器返回的最后修改时间。服务器比较这两个时间，如果它们相同，则返回 304，否则返回新的资源并更新最后修改的资源。

## ETag

HTTP/1.1 中的一个新字段表示文件的唯一标识符。只要文件内容改变，ETag 就会重新计算。缓存过程与 Last-Modified 相同:服务器发送 ETag 字段->浏览器再次请求时发送 If-None-Match->如果 ETag 值不匹配，则文件已更改，返回新资源并更新 ETag，如果匹配，则返回 304。

## 最后修改的和 ETag 的比较

ETag 比 Last-Modified 更准确:如果我们打开文件不做修改，Last-Modified 也会发生变化，Last-Modified 的单位时间是一秒。如果文件在一秒钟内被修改，它仍然会命中缓存。
如果没有设置缓存策略，浏览器会将响应头中的日期减去上次修改值的 10%作为缓存时间。

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----21cd081886d--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----21cd081886d--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----21cd081886d--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----21cd081886d--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----21cd081886d--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----21cd081886d--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*