# 角度与反应

> 原文：<https://javascript.plainenglish.io/angular-vs-react-c07cc7711423?source=collection_archive---------4----------------------->

## web 开发人员的一个有保证的面试问题。

![](img/e141ae48d3021206d779d0a82156bb9c.png)

Photo by [Bogdan Yukhymchuk](https://unsplash.com/@yuhy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近，我一直在思考一些面试问题，这些问题在今年夏天我本可以回答得更好。特别是在一次面试中，有人问我能否解释 Angular 和 React 之间的区别。在那之前，我有过在几个不同的项目中使用 Angular 的经验，但是相比之下，使用 React 的经验很少。基本上，你可以想象，我对这个问题没有一个完整的答案。但这让我想到，寻找差异可能会成为一篇有趣的文章，或者对任何想了解差异的人有所帮助。

因此，在本文中，我们将了解 Angular 和 React 之间的一些主要差异。

# **成分差异**

我们要看的第一个差异是架构上的差异。Angular 是作为一个完整的框架构建的，用 TypeScript 编写。它是由谷歌开发和维护的。就其本身而言，Angular 也是一个完整的解决方案。因为它是一个完整的框架，所以它是控制流程的框架。这意味着您插入您需要的代码，但是 Angular 决定何时调用代码。Angular 在架构上也是基于组件的。这遵循 MVC(模型、视图、控制器)框架。Angular 被认为是一个框架，因为它为应用程序提供了强大的功能，比如结构、模板和单元测试工具。

另一方面，React 不是一个框架。相反，它是一个 JavaScript 库。React 也可以与其他编程库打包在一起，因为它本身并不是一个完整的解决方案。因为 React 只是一个库，所以您控制着应用程序的流程。这意味着您决定何时调用代码或集成库。React 是由一个来自脸书的开发者创建的，目前由 Meta 维护。

Angular 和 React 的另一个区别是它是常规的还是虚拟的 DOM(文档对象模型)。本质上，DOM 是一个表示 HTML 和 XML 文档页面的接口，因此程序可以改变结构、样式和内容。因为 Angular 使用常规 DOM，所以当结构或内容改变时，HTML 标记的整个树结构都会更新。正常情况下，当它只是一个小项目时，它应该不是一个问题。但是，如果在同一个页面上有大量的数据请求，每个页面请求都要替换 HTML，那么这会对性能产生负面影响。并且较慢的性能也会损害用户的性能。

React 使用虚拟 DOM，这是常规 DOM 的一种更快的替代方案。虚拟 DOM 更新 HTML 代码块中的特定部分，而不是整个树结构。为此，它会比较以前和当前的 HTML，然后只在必要的地方进行更改。

数据绑定是两者之间可以进行的另一种比较。Angular 使用双向数据绑定。这意味着当模型状态改变时，UI 元素也会改变。如果 UI 元素发生变化，那么相应的模型状态也会发生变化。这显示了双向数据绑定。在 React 中，只有单向数据绑定。如果模型状态被更改，那么 UI 元素也会被更新。但是，如果更改了 UI 元素，模型状态不会改变。这显示了单向数据绑定。

# **灵活性和易用性**

在考虑易用性时，你不得不考虑学习曲线。然而，从我的阅读和个人经验来看，仅仅因为一个比另一个“容易”并不一定就容易学。“更容易”，是的，但与其他框架/库相比并不总是很容易。

我提出这个问题的原因是，与整个框架相比，React 只是一个库，比 Angular 更容易学习。React 的学习曲线要少得多，但可能也很困难，比如当它用 Redux 增强时。

然而，一旦您习惯了语法，Angular 并不太难。这对初学者来说很难，需要时间和训练，但是一旦你习惯了，就不会比最初的学习更难了。根据我的经验，React 也需要一点时间来适应，但是与 Angular 相比，React 有一个更容易的学习曲线。

Angular 和 React 都比旧技术快，但 React 会更快，因为它是轻量级的。这也与尺寸有关，其中 Angular 更大，因此需要更长的加载时间，特别是影响移动性能。

相比之下，React 更小，因此速度更快。Angular 和 React 都很容易缩放，React 由于其灵活性比 Angular 更容易缩放。说到灵活性，与 React 相比，Angular 只提供了有限的自由度和灵活性，因为 React 让您能够选择使用哪些工具、库和架构进行开发。

然而，作为一个小图书馆也有一些缺点。有单向数据绑定，但测试和调试工具也不容易获得。对于 React，您必须使用一套工具来进行不同类型的测试。有了角度，只用一个工具就可以进行完整的测试。

安装 Angular 时，设置起来相当容易。然而，它更大，一旦你开始编码，就有更多的元素要处理。这意味着可能会有更多的编码时间。另一方面，React 需要更长的时间来设置。尽管这需要更长的时间，但需要担心的元素更少，因此您可以更快地启动和运行代码。

了解了他们的背景和能力之后，让我们看看使用框架或库的一些优点。

# **React 和 Angular 的优点**

使用 Angular 的一个优点是其更高的性能和结构。它还可以使用 Angular CLI 无缝更新。因为是框架，所以也有干净的代码开发，以及负责路由。这使得从一个视图切换到另一个视图变得更加容易。

与 Angular 相比，使用 React 的一个优点是由于其简单的设计而易于学习。您在使用 React 时学到的任何技能也可以应用于本机开发。增强了对服务器端呈现的支持，这使得它对于以内容为中心的应用程序来说非常健壮。因为 React 只是一个库，开发人员不必太担心特定于框架的代码，而是可以专注于编写代码所需的 JavaScript。语法也类似于 HTML，这使得编写详细的文档或模板更加容易。

有了一些优点，让我们也看看两者的一些缺点。

# **反应过来的缺点和棱角**

Angular 的一个缺点是，一开始学习这个框架可能会很困难或者很混乱。也没有广泛/包罗万象的文件。有了 Angular，第三方集成就困难了。从旧版本切换到新版本时，您可能也会遇到问题。Angular 也很大，这可能意味着它比较慢，尤其是当页面嵌入了交互元素时。

React 的一个缺点是它只是一个库，因此将它与传统的 MVC 框架集成在一起配置起来很复杂。您还必须深入了解用户界面集成的 MVC 框架。如前所述，您还需要针对不同测试用例或调试技术的各种工具。

# **结论**

今天，我决定最终了解 Angular 和 React 之间的区别。正如我们所见，最大的区别在于 Angular 是一个完整的框架，而 React 是一个库。我们关注的其他差异包括组成、易用性、可伸缩性、整体结构等等。一旦我们确定了主要的不同点，我们也看了两者的一些优点和缺点。

总的来说，我觉得我更好地理解了两者的区别，并且现在更好地准备回答我以前无法自信地回答的面试问题。希望你也认为这是一本有趣的读物。下次见，干杯！

***用我的*** [***每周简讯***](https://crafty-leader-2062.ck.page/8f8bcfb181) ***免费阅读我的所有文章，谢谢！***

***想看完介质上的所有文章？成为中等*** [***成员***](https://miketechgame.medium.com/membership) ***今天！***

*看看我最近的一些文章:*

[](https://medium.com/codex/how-to-host-your-own-docker-registry-58569f317582) [## 如何托管自己的 Docker 注册表

### 退出 Kubernetes Kubeadm，转而使用 MicroK8s 第二部分

medium.com](https://medium.com/codex/how-to-host-your-own-docker-registry-58569f317582) [](https://medium.com/codex/how-i-learned-to-write-solid-code-529f5b840b0) [## 我如何学会编写可靠的代码

### 学习面向对象的设计原则

medium.com](https://medium.com/codex/how-i-learned-to-write-solid-code-529f5b840b0) [](https://miketechgame.medium.com/byoe-imagining-the-future-of-workplaces-3d3d088dcd27) [## BYOE——想象工作场所的未来

### 如何带来你自己的环境可能正在改变公司文化

miketechgame.medium.com](https://miketechgame.medium.com/byoe-imagining-the-future-of-workplaces-3d3d088dcd27) [](https://towardsdatascience.com/the-ethics-of-data-science-55bcba9b4ecb) [## 数据科学的伦理

### 大数据:合理使用还是潜在侵犯隐私？

towardsdatascience.com](https://towardsdatascience.com/the-ethics-of-data-science-55bcba9b4ecb) [](https://towardsdatascience.com/all-about-deepfakes-e481a55cf7e5) [## 关于 Deepfakes 的一切

### 什么是 deepfake，它在当今世界有多“真实”？

towardsdatascience.com](https://towardsdatascience.com/all-about-deepfakes-e481a55cf7e5) 

参考资料:

 [## 角度与反应-Java point

### Angular 和 React 都与 JavaScript 相关，但它们之间有很多不同之处。在这里，我们将…

www.javatpoint.com](https://www.javatpoint.com/angular-vs-react) [](https://trio.dev/blog/angular-vs-react) [## 2022 年 Angular 与 React:并排比较

### 探索 Angular 与 React 之间的基本技术和质量差异及其各自的优势和…

trio.dev](https://trio.dev/blog/angular-vs-react) [](https://www.guru99.com/react-vs-angular-key-difference.html#:~:text=Angular%20JS%20is%20based%20on%20MVC%20%28Model%20View,allows%20adding%20javascript%20library%20to%20the%20source%20code) [## 反应与角度:你必须知道的 10 个最重要的区别！

### React JS 是什么？React 是一个由脸书开发的 Javascript 库，它允许你构建 UI 组件。它…

www.guru99.com](https://www.guru99.com/react-vs-angular-key-difference.html#:~:text=Angular%20JS%20is%20based%20on%20MVC%20%28Model%20View,allows%20adding%20javascript%20library%20to%20the%20source%20code) 

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*