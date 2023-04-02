# 用普通的 JavaScript 向任何类添加事件

> 原文：<https://javascript.plainenglish.io/add-events-to-any-class-in-vanilla-javascript-1b3805e5740b?source=collection_archive---------2----------------------->

## 当编写更大的应用程序时，让组件交互的最好方法之一是以一种松散耦合的方式分派和使用事件。

![](img/d96aa806d36ddc18ca1f73942b679e12.png)

这在 web 组件中非常适用，因为它们基于 DOM 元素，并且内置了事件。

然而，在常规的 **ECMAScript** 类中，您将不得不回归到开发您自己的发布/订阅系统。不是火箭科学，但仍然有点管道工程…

但是有一个更简单的解决方案。通过使用`createDocumentFragment()`，让 DOM 为您处理它。

这个小小的 **Events** 类使得任何类都成为事件生成类:

这种方法的唯一缺点是监听器不能直接使用`event.target`，因为它指向文档片段。

我使用的解决方法是在片段上设置一个**主机**属性，这样您就可以使用`event.target.host`。

使用 Events 类很简单:

简而言之， **Events** 类将片段的事件方法委托给 host 类。

`emit()`和`on()`方法只是方便的快捷方式，而`on()`的额外好处是它是可链接的:

慢慢来。

我在任何地方都用这个。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*