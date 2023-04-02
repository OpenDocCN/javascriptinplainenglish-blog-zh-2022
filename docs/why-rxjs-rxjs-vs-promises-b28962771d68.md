# 为什么是 RxJS？RxJS vs 承诺

> 原文：<https://javascript.plainenglish.io/why-rxjs-rxjs-vs-promises-b28962771d68?source=collection_archive---------6----------------------->

## [RxJS](https://medium.com/@lorenzozar/list/rxjs-39bc4f4110ec)

![](img/2b1d4527bb57ba79e40b9572293a0cda.png)

A clear statement about this post

RxJS 是一个帮助我们管理和操作数据的库。通常，这涉及到异步操作。

尽管有其他技术来管理异步和基于事件的数据，我们可能还是想使用 RxJS。

下面，我将简要回顾一些处理异步和基于事件的数据的传统技术。之后我会和 RxJS 对比那些技术。

# 传统技术

## 回调函数

异步操作完成后回调函数。当处理许多异步操作或者这些操作相互嵌套时，回调可能很难管理。你可能想避免回调地狱。

## 承诺

"*承诺对象表示异步操作的最终完成(或失败)及其结果值*， [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 。但是，承诺只能处理一个值，并且不可取消。

## 异步/等待

"*async 和 await 关键字使异步的、基于承诺的行为能够以更简洁的方式编写，避免了显式配置承诺链*， [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) 。

正如 MDN 上所报道的，async/await 的"*目的是简化使用基于承诺的 API 所必需的语法。*“因此，async/await 是基于承诺的，这种语法具有与承诺相同的特征。

Async/await 只能处理一次发射，并且不可取消。

# RxJS(可观察到的)与承诺

尽管还没有介绍[可观的东西](https://www.vitainbeta.org/2022/02/01/what-are-observables/)，我们可以把可观的东西看作“RxJS 的承诺”。目前，这已经足够了。我们将很快引入 Observables。

由于 RxJS 是一个库，所以不能拿 RxJS 和 Promises 比较。然而，可以将“RxJS 的承诺”，即可观察到的承诺，与传统的承诺进行比较。

正如 [angular.io](https://angular.io/guide/comparing-observables#observables-compared-to-promises) 所报道的，可观察到的和承诺之间有一些关键的区别。

虽然承诺返回一个值，但可观测量可以提供多个值。*这使得 observables 对于随时间推移获取多个值非常有用*。

虽然承诺在创造时就开始执行，但可观察的事物直到我们想要它们开始时才会开始执行。为了调用一个可观察对象并获得一个或多个值，我们需要*订阅*它。可观察的东西是懒惰的，承诺不是。

还有更多的不同，但这些足以得出一些结论，为什么 RxJS 可能比传统的承诺更受欢迎。

# 为什么是 RxJS？

使用 RxJS 有几个好处。

*   **一库多用**。我们可以使用一个库，通过相同的操作符来处理任何类型的数据。例如多个数据源、事件发射器和 API。
*   **作文**。我们可以随心所欲地将几个来源的数据结合起来。
*   **警惕的**。随着时间的推移，RxJS 可以产生多个值，当特定事件发生时，它使用推送模型来通知我们。这允许进行反应式编程，因为可以观察用户的动作和变化并对其做出反应。
*   **懒散**。评估直到订阅才开始。
*   **内置错误处理**
*   **可取消**。与承诺不同，取消异步操作是可能的。

接下来:[什么是 RxJS 可观测量？](https://medium.com/p/5707e0c4c7ba)

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*