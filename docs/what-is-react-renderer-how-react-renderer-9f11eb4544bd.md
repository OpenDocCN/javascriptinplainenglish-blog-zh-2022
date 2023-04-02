# React 如何渲染 React 元素

> 原文：<https://javascript.plainenglish.io/what-is-react-renderer-how-react-renderer-9f11eb4544bd?source=collection_archive---------3----------------------->

## 什么是 React 渲染器？React 渲染器是如何工作的？从创建 React 元素到用户界面的过程。什么是反应元素？

![](img/0f9c0d92cb438f4e0b746cbc80807c72.png)

React Native 是一个框架，允许我们使用 React 库开发移动应用程序。这篇博文是 React Native 的第一部分，它解释了 React 在编程运行时是如何工作的，并深入 React 的渲染器。

简而言之，React 是一个库，它允许我们使用 Javascript 编程语言以声明方式轻松地生成交互式 ui。目前(2022 年 11 月 6 日)，它是使用最多的 UI 框架，每周下载 190220699 次。当我们观察 React 的工作机制时，我们可以将其分为 3 个基本特征；核心、调解和呈现者。在快速查看了核心和协调之后，我们将进一步了解 Renderer，以帮助我们更好地理解 React Native。

## **T3 . a .核心:T5**

核心与每个 React 项目共享，不管环境如何(移动、Web、桌面等)。).诸如状态、道具、效果、背景、备忘录等特征。都被核心所覆盖。

## ***b .对账:***

**对账**是 React 更新浏览器 DOM 的过程。当组件中有任何状态改变时，它是计算诸如 DOM 是否应该被改变或者 DOM 中的哪个元素将被改变的算法。这些操作是使用虚拟 DOM 完成的。React 表现好的原因在于这个算法的工作方式。

## **c .渲染器:**

***React 元素:*** React 元素是 React 的最小积木，是一个普通的 Javascript 对象。作为一个例子，我们来看看 React 元素是什么样子的。

`{ type: 'button', props: {className: 'btn-primary'}}`

一个简单的 React 元素如上。它有两个属性。一个是渲染器将理解的类型和它将接收的道具的道具属性。那么，我们如何将嵌套的 React 元素创建为树，而不仅仅是单个 React 元素，并将其形状保存在 DOM 中呢？让我给你一个提示，还记得每个 React 组件中的儿童道具吗？让我们向您展示如何快速创建它。

`{type: 'main', props: {children: [{type: 'article', className: 'container'}, {type: 'footer'}]}`

既然我们已经学习了 React 元素，我们将能够更容易地学习渲染器的工作机制。渲染器是根据 React 应用程序中的主机环境(Web、移动、桌面等)了解差异并根据该主机环境渲染 React 元素或使其能够处理该环境的事件的层。两个最常用的例子是:Web 上 React DOM(主机环境)，Android 和 IOS 上 React Native(主机环境)。

React 渲染器有两种不同的模式，变异和持久。变异模式是最常用的渲染器模式。这种模式像 DOM 一样工作。它创建一个节点，设置属性，并添加和移除其子节点。当主机环境不支持某些方法时，使用持久模式。不可变。

开发我们的自定义渲染将有助于我们更好地理解这个主题。为此，你可以在 [ReactConf 2019](https://www.youtube.com/watch?v=CGpMlWVcHok) 上查看[‘索菲·阿尔珀特’](https://sophiebits.com/)清晰而令人印象深刻的演示。在本演示中，Sophie 正在开发一个迷你 ReactDOM 库，其功能包括将 React 元素添加到 DOM 中，在状态改变时更新 DOM，添加 onClick 事件，并使用 DOM 中的对应项生成某些道具。在此，我想对索菲·阿尔珀特表示感谢。这真是一场令人印象深刻的演讲。观看视频，不要错过申请。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***