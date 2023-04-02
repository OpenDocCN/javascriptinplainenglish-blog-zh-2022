# 新 React 文档:不要滥用效果

> 原文：<https://javascript.plainenglish.io/the-new-react-document-dont-abuse-effect-2ee10a6b4718?source=collection_archive---------6----------------------->

![](img/265272ac6dc148c68858b1b222f0ff86.png)

Photo by [John Bakator](https://unsplash.com/@jxb511?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当您或您的同事使用 useEffect 挂钩时，是否出现过以下情况？

当你想在状态 A 改变后“发起一个请求”时，你使用 useEffect:

代码如预期的那样工作，并且在上线时很好。

随着需求的迭代，状态 A 在别处被修改。但是在那个需求中，不需要在状态 A 改变之后发起请求。

你不想碰前面的代码，所以你要重新修复 bug，所以你加了一个判断条件:

有一天，要求又变了！现在请求还需要 B 字段。

这很简单，您只需添加 b 作为 useEffect 依赖项:

随着时间的推移，你会发现:

“是否发送请求”与“如果条件”相关

“是否发送请求”还与“A、B 等依赖关系”有关

“像 A 和 B 这样的依赖关系”与“许多需求”相关

知道请求什么时候发，好混乱…

如果这些听起来很熟悉，那么 React 文档显然提供了一个解决方案。

## 一些理论知识

新文档的这一部分称为与效果同步[1]，目前处于草稿状态。

但是 React 开发人员应该了解一些概念。

首先，关于效果的部分属于逃生舱一章[2]。
顾名思义，开发者不一定需要使用 Effect，它只是特殊情况下的逃生舱。

React 有两个重要的概念:

*   渲染代码
*   事件处理程序

渲染代码指的是“开发者对组件的渲染逻辑”，将返回一片 JSX。

例如，以下组件内部有呈现代码:

渲染代码被定义为“没有副作用的纯函数”。

以下呈现代码包含副作用(计数更改)，不推荐使用:

## 处理副作用

事件处理程序是“包含在组件中的函数”，它执行用户操作，并且可能包含副作用。

下列操作属于事件处理程序:

*   更新输入字段
*   提交表单
*   导航到其他页面

以下示例中组件内的 changeName 方法属于事件处理程序:

然而，并不是所有的副作用都可以在事件处理程序中处理。

例如，在聊天室中,“发送消息”是由用户触发的，应该由事件处理程序来处理。

另外，聊天室需要时刻保持与服务器的长时间连接。“保持长时间连接”的行为是一种副作用，但不是由用户的行为触发的。

视图呈现后触发的效果是效果，应该由 useEffect 处理。

回到开头的例子:

当您想在状态 A 改变后“发起请求”时，您应该首先明确您的要求是:

“状态 A 改变，下一步需要发起请求”

或者

“用户操作需要发起一个依赖于状态 A 作为参数的请求”？

如果是后者，这是用户动作触发的副作用，那么相关逻辑应该放在事件处理程序中。

假设前面的代码逻辑是:

*   点击按钮触发状态 A 改变
*   UseEffect 执行并发送请求

应该改为:

*   单击按钮以获取事件回调中状态 A 的值
*   在事件回调中发送请求

此次修改后，“状态 A 改变”与“发送请求”之间不存在因果关系，后续对状态 A 的修改也不存在“无意中触发请求”的顾虑。

## 结论

当我们写组件时，我们应该尽量把它们写成纯函数。

对于组件中的副作用，首先应该明确:

是“用户动作触发”还是“视图渲染主动触发”？

对于前者，逻辑在事件处理程序中处理。

对于后者，使用 useEffect 处理。

这就是为什么 useEffect 部分在新文档中被称为 Escape Hatches 在大多数情况下，您并不使用 useEffect，它只是在没有其他应用时的一个逃生舱。

**感谢阅读这里！**

***期待您的关注！***

## 资源

[1]与效果同步:[https://beta-react js-org-git-Effects-fbopensource . vercel . app/learn/Synchronizing-with-Effects](https://beta-reactjs-org-git-effects-fbopensource.vercel.app/learn/synchronizing-with-effects)

[2]Escape Hatches:[https://beta-react js-org-git-effects-fbopensource . vercel . app/learn/Escape-Hatches](https://beta-reactjs-org-git-effects-fbopensource.vercel.app/learn/escape-hatches)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*