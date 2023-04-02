# Redux 的实现原理

> 原文：<https://javascript.plainenglish.io/implementation-principle-of-redux-7fe49a912960?source=collection_archive---------13----------------------->

## 我们为什么需要`Redux`，`Redux`为我们解决了什么问题？

![](img/537f3a86aa8a0300bb6abd3938668c9e.png)

Photo by [Cristian Castillo](https://unsplash.com/@castillcc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在一切开始之前，我们首先要回答一个问题:我们为什么需要`redux`,`redux`为我们解决了什么问题？只有回答了这个问题，才能把握`redux`的设计思路。

作为一个基于组件的开发框架，组件之间有大量的通信。有时这些通信跨越多个组件，或者在多个组件之间共享一组数据。简单的父子组件值传递无法满足我们的需求。自然，我们需要一个地方来访问和操纵这个公共状态。而`redux`为我们提供了管理公共状态的解决方案，我们后续的设计和实现也将围绕这一需求。

我们来思考一下如何管理公共状态:既然是公共状态，那么我们可以直接提取公共状态。我们创建一个`store.js`文件，然后将公共状态直接存储在其中。其他组件只要导入该存储，就可以访问共享状态。

```
const state = {    
    count: 0
}
```

我们在存储中存储一个公共状态计数，组件可以在导入存储后操作这个计数。这是最直接的商店。当然，我们的店一定不能这么设计。有两个主要原因:

*   **很容易误用。**比如有人不小心把`{}`的值赋给了商店，清空了商店，或者误修改了其他组件的数据，都是不安全的，而且很难排查错误，所以我们需要有条件直接操作商店，防止用户直接修改商店的数据。
*   **可读性差 JS 是一种非常依赖语义的语言。**试想一下，如果不加注释直接在代码中修改公共状态，以后其他人维护代码会更加迷茫。为了理解修改状态的含义，还必须从上下文中进行推断，所以我们最好给每个操作取一个名字。

让我们重新思考如何设计这个公共状态管理器。根据我们上面的分析，我们希望公共状态可以全局访问，私有状态不能直接修改。想想这个闭包是不是正好适合这个。有两个要求，所以我们将公共状态设计为闭包(理解闭包有困难的同学也可以跳过闭包，不影响后续理解)。

因为我们想要访问状态，所以必须有 getters 和 setters，当状态改变时，我们必须广播通知组件状态已经改变。这不就对应了`redux` : `getState, dispatch, and subscribe`三个 API 吗？我们用几行代码勾勒出商店的大致形状:

# 1.getState()实现

`getState()`的实现很简单，只需返回当前状态:

# 2.dispatch()实现

我们必须考虑`dispatch()`的实施。经过上面的分析，我们的目标是有条件地修改门店数据，那么我们如何实现这两点呢？我们已经知道，在使用 dispatch 时，我们会向`dispatch()`传递一个 action 对象，这个对象包含了我们要修改的状态和操作的名称(actionType)。根据不同的类型，商店将修改相应的状态。我们在这里也使用这种设计:

我们在 dispatch 里面写了`actionType`的判断，非常臃肿笨拙，于是想到把修改状态的这部分规则提取出来放在外面，也就是我们熟悉的 reducer。让我们修改代码，让减速器从外部传入:

然后我们创建一个`reducer.js`文件并编写我们的 reducer:

代码写到这里，我们可以验证`getState`和`dispatch`:

运行代码，我们会发现打印的状态是:`{ count: NaN }`，这是因为存储中的初始数据是空的，`state.count + 1`实际上是`underfind+1`，而`NaN`是输出，所以我们要先做存储数据初始化，我们在执行`dispatch ({ type: ‘plus’ })`之前执行一个初始化的调度，这个调度的`actionType`可以随意填充，只要它不重复现有的类型，这样 reducer 中的开关就可以默认地去初始化存储:

# 3.subscribe()实现

虽然我们已经能够访问公共状态，但是存储的改变不会直接引起视图的更新。我们需要监控商店的变化。这里我们应用了一个设计模式——观察者模式。观察者模式广泛用于监控事件。实现(有些地方写的是发布订阅模式，但我觉得这里叫观察者模式更准确。关于观察者和发布订阅的区别有很多讨论，读者可以搜索)。

所谓观察者模式，概念也很简单:观察者监听观察到的变化，当观察到变化时通知所有观察者。那么，我们如何实现这个监控-通知功能呢？为了照顾到不熟悉观察者模式实现的同学，我们跳出`redux`来写一个简单的观察者模式实现代码:

解释一下上面的代码:observer 对象有一个 update 方法(收到通知后要执行的方法)，我们想在 observer 发送通知后执行这个方法；观察者有`addObserver`和【notify】方法，`addObserver`用来收集观察者，它是将观察者的更新方法加入到一个队列中，当执行 notify 时，所有观察者的更新方法都从队列中取出来执行，从而实现通知的功能。我们的`redux`监控通知功能也将按照这个实现思路实现`subscribe`:

有了上面观察者模式的例子，`subscribe`的实现就应该很好理解了。在这里，dispatch 和 notify 被合并。每次调度时，我们都广播通知组件库状态已经改变。

我们试试这个`subscribe`(不需要创建一个组件然后把商店介绍给`subscribe`，直接在`store.js`中模拟两个组件使用`subscribe`订阅商店变化):

至此，一个简单的`redux`已经完成，参数验证等细节也加入到了`redux`的真实源代码中，但大致思路同上。

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----7fe49a912960--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----7fe49a912960--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----7fe49a912960--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----7fe49a912960--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----7fe49a912960--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----7fe49a912960--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***