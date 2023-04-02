# 每个人对反应母语情态动词的误解

> 原文：<https://javascript.plainenglish.io/you-have-been-using-react-native-modals-wrong-9b8c17de2f96?source=collection_archive---------1----------------------->

## 如何掌握反应原生模态复合流的指南。

![](img/654d479d97ffb569d8b91c173a07c7a5.png)

[https://gifs.com/gif/this-is-fine-qj5Dv2](https://gifs.com/gif/this-is-fine-qj5Dv2)

您是否发现在 React Native 中使用情态动词有点麻烦？你并不孤单！试图保持对其开放状态的控制并在任何你想使用它的地方重复代码可能是相当乏味的。

当您试图创建复杂的流时，问题只会变得更糟。一旦你通过了两个模态，你的主要部分就是一团乱麻，状态无处不在。

我在许多大公司都亲身经历过，比如 **Zé Delivery** (由 AB-InBev 公司生产)、 **Alfred Delivery** ，现在在 **X-Team** 。

但不要绝望！大多数人认为这是唯一的方法。尽管如此，在本文中，我将解释问题是如何开始的，以及如何优雅地处理它们，同时提高您的开发经验。它甚至会帮助你使用内外反应成分的情态动词(例如在[实录](https://redux-saga.js.org/)中)！)

*本文的教导已封装在此库中:*

[](https://github.com/GSTJ/react-native-magic-modal) [## 反应自然魔法模式🦄

### 一个可以在任何地方被强制调用的模态库！

https://github.com/GSTJ/react-native-magic-modal](https://github.com/GSTJ/react-native-magic-modal) 

# “简单流程”的挑战

想象一下。您在脸书工作，产品团队要求“简单流程”:

> 作为一家公司，我想展示一种模式，要求用户在第一次喜欢一篇帖子后，对该应用进行 0-5 星级的评分。
> 
> a.**如果用户给它的评分少于四颗星，则**显示另一种模式，询问如何改进。
> 
> b.**否则，**会显示一个快乐的模式，要求用户在应用商店给我们打分。
> 
> **最后**展示一个“谢谢”的模式，感谢用户的支持。

这不是很牵强，对吧？

四种模式，它从开发者的角度提出了很多问题。这个逻辑应该放在哪里？我们应该如何处理最后一个模态的输出？我们如何保持清洁？

你能认出密码是什么吗？您是否看到自己在编写复杂的逻辑来处理模态的顺序，确保每个模态都已经转变为不可见，并且有大量的 *useStates* 在适当的位置？

## 问题的发展

想象你最终做到了，你完成了流程，产品团队喜欢这个结果！他们现在想扩展这一流程，使其在用户第一次喜欢任何东西时只出现一次，无论是帖子、评论还是产品。您会如何处理？

你必须在每一个可能喜欢的屏幕上复制粘贴这四种模式。也许您甚至可以将所有这些都集成到一个组件中。即便如此，仍然需要将这个包装组件添加到每个屏幕上。

几个月过去了，开发团队现在看到了在每个屏幕上不同地处理 likes 的复杂性，并希望将这一责任移交给可以在任何地方调用的 [Redux Saga](https://redux-saga.js.org/) 。如何在[传奇的动作](https://redux.js.org/tutorials/fundamentals/part-3-state-actions-reducers)开火时才显示模态？ [Sagas](https://redux-saga.js.org/) 运行外 React 组件。

我可以自信地说，我经历过那些场景的发生。在食品配送行业工作，我们一直要求用户对应用程序、配送和他们的购买进行评级。

# 如何避免？

让我们从解决国家问题开始。管理它是使用模态时最重要的事情之一。

## 用" *useImperativeHandle"* 公开内部属性

简而言之，[*useImperativeHandle*](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)允许你通过 Ref 公开内部属性。如果你有一个模态组件，你可以使用[*useImperativeHandle*](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)来公开它们的“ *show* ”和“ *hide* ”函数。意思是它可以管理自己的状态，而不用委托给它的父组件，例如用 [*道具*](https://reactnative.dev/docs/props) 。

当你想让你的代码更清晰并避免传递许多道具时，这是很有帮助的。让我们试一试:

That’s the transition to a better place.

虽然这是朝着正确方向迈出的一步，但它本身并不能解决我们所有的问题。即:

*   要使用它，我们需要从一个 [*useRef*](https://reactjs.org/docs/hooks-reference.html#useref) 钩子传递一个*‘ref’*prop，这意味着我们不能在 React 组件之外调用‘show’。
*   我们仍然需要在每个屏幕上实例化组件。如果不重复使用*示例模式*，就无法在多个屏幕上使用它。

## 向外公开组件的引用

大多数人不知道这一点，但是 React 有一个 [*createRef*](http://reactjs.org/docs/refs-and-the-dom.html#creating-refs) 方法，可以在 React 组件之外使用。事实上，它甚至出现在针对边缘情况的 React-Navigation 文档中。

[*https://react navigation . org/docs/navigation-with-navigation-prop/*](https://reactnavigation.org/docs/navigating-without-navigation-prop/)

在实践中，它带来的灵活性可以在这里看到:

现在*祈使句*可以导入到任何地方使用，只要*智能示例*在根目录下。我们可以使用*显示*和*隐藏*来隐藏每个组件、功能或[传奇](https://redux-saga.js.org/)。

这解决了我们的大多数问题，但是还有一个问题:很难管理一个有很多模态引用和模态的项目。

在那里，您可以通过抽象进行创作，使*智能示例*呈现您想要的任何模式！一种方法是让 *show* 函数接收一个组件并渲染它。

# 走得更远

我没有让你们重新发明轮子，而是基于[*react-native-modal*](https://github.com/react-native-modal/react-native-modal)创建了一个开源库，该库封装了所有这些概念以及更多概念，并提供了完整的 TypeScript 支持。

以下是如何使用它的基本想法:

> “说话便宜。**给我看看代码**。― **Linus Torvalds** 。

Example using react-native-magic-modal

正如您所看到的，通过简单地抽象我们已经经历过的概念，它给了您很多以前无法想象的灵活性。

现在，确认流程可以从任意位置调用。内部或外部反应部件。

此外，它还自动处理关于情态动词的常见问题。

> **你知道在《自然反应》中，不能同时出现两种情态动词吗？**
> 
> 即使您试图一个接一个地显示一个模态，也可能会失败，因为最后一个模态仍然处于“关闭”状态。幸运的是，我们这边已经解决了这个问题。
> 
> [https://git hub . com/react-native-modal/react-native-modal/issues/30](https://github.com/react-native-modal/react-native-modal/issues/30)

React Native Magic Modal 文档很容易理解，会让您有一个开始。您可以在这里了解更多信息:

[](https://github.com/GSTJ/react-native-magic-modal) [## 反应自然魔法模式🦄

### 一个可以在任何地方强制使用的模态组件！

github.com/GSTJ/react-native-magic-modal](https://github.com/GSTJ/react-native-magic-modal) 

同样的逻辑已经在我工作过的大公司中经受了考验，比如 **Zé Delivery** (由 AB-InBev 生产)、 **Alfred Delivery** 、以及 **X-Team** 。

接受捐款！

*感谢阅读。如果你喜欢这篇文章，请关注我的* [*Linkedin*](https://www.linkedin.com/in/gabrieltaveira/) *和*[*Github*](https://github.com/GSTJ)*。*

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***