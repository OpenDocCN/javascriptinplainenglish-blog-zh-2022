# 魔女之歌——前端框架如何不断引诱您陷入技术债务

> 原文：<https://javascript.plainenglish.io/song-of-the-siren-how-frontend-frameworks-keep-luring-you-into-technical-debt-a7e8b7300f33?source=collection_archive---------11----------------------->

![](img/65be8f2eda120a3e8b7cb7998862a1c2.png)

Santiago Alvarez — The siren song — Flickr

> 我怀疑许多开发人员使用框架来避免学习 DOM 和类似的东西，但是最终却不断地跟上[短暂有价值的技能集](http://blog.teamtreehouse.com/wp-content/uploads/2015/08/react-hype.jpg)而不仅仅是学习底层的 API。— [埃里克·瓦斯特](https://softwareengineering.stackexchange.com/users/197926/eric-wastl)

如今，非常常见的是，前端开发人员空缺需要 reactor、Vue.js 或 Angular 经验，甚至不提 JavaScript。

因此，与其要求对本地网络技术有深入的了解和经验，不如要求人们熟练掌握多变的第三方框架 *du-jour* 。

> 学会耐心，而不是新的框架——[Sunny Singh](https://dev.to/sunnysingh)

## 炒作周期

我参与过相当多的初创公司，他们中的大多数人在选择前端框架后才开始考虑技术要求…

历史不断重演。问问真正的老年人，他们会回忆起许多框架的兴衰。

## 迟发性疼痛

问问曾经去过*并完成过*的工程经理和首席技术官，他们会告诉你**交付后 2-3 年框架带来的痛苦和障碍**。

> 所有的大型框架都附带有**魔女之歌**:你的第一行代码承诺了快速的进步和节省时间，但是在某些时候，平衡会发生变化，收益会变成损失。

当框架中使用的抽象层很难找出问题的根本原因时，就会发生这种情况。

或者当“攀比”是一件事的时候，比如当你看到你选择的框架有了新的版本，或者当你想使用某个插件，但是它和你使用的框架版本不兼容的时候。但是升级框架也是一个麻烦和风险。免费技术债务。谁不想这样？

例如，我记得 2016 年 AngularJS 到 Angular2 的突破性变化，以及我的团队因为不得不基本上重做 Angular2 中的所有代码而经历的重大挫折。

就在最近，我的一个使用 *Vuetify* 组件系统的客户决定放弃它，改用一个新的，因为它还不支持 Vue3。

有大量的例子表明，锁定一个生态系统会导致重大痛苦。

> 此外，从首席技术官的角度来看，我可能会补充说，我也看到很多决策都在公司的“雷达”之下，但是选择的财务影响是如此明显，你应该把它们考虑进去。

如果我们最终只是从简单开始，只有当我们看到附加值时才添加额外的工具/框架，会怎么样？

# 那我们该怎么办？

## 1.要耐心

首先，正如我之前所说，在采用一些新的闪亮的框架之前，耐心是必不可少的。

“对于任何你希望至少持续 5 年的大项目，在决定学习和使用它之前，你可能希望观察一个框架的社区足够长的时间。把你花在学习特定框架或工具上的时间当作一种投资。”— [桑尼·辛格](https://dev.to/sunnysingh/investing-in-the-right-technologies-to-avoid-technical-debt-2c06)。

## 2.把它作为一个商业决策

此外，正如我所指出的，考虑到超出开发人员热衷强调的技术优势的高层次因素，将框架选择作为一个**商业决策**确实是有意义的。毕竟，如果过了一段时间，您的团队因为 NPM 依赖地狱、不兼容的组件升级或复杂的重构而陷入严重的困境，那么业务就会受到影响。

## 3.务实点

接下来，我不断重复这一点:你可能不是脸书，也永远不会有像脸书或其他几个人这样复杂和沉重的前端。
这意味着这些框架存在的一些原因(例如跨数百个组件的反应状态保持)可能不需要在你的应用中解决。

## 4.接受事实

如果你决定使用一个框架，接受从那时起，框架调用你的代码，你的代码调用库。

当你决定使用一个框架时，你不仅不再能完全控制。此外，当问题发生时，追溯到底是什么出了问题会更加昂贵，因为当今的框架中有许多抽象层。随着框架升级，抽象层可以很容易地改变。

当一个框架寿终正寝时，你会面临一个非常棘手的问题。有了原生 Web 技术，[情况好了很多，](https://www.w3.org/People/Bos/DesignGuide/compatibility.html)尽管开发人员抱怨 HTML 和 JavaScript 中仍然存在极其陈旧的结构。

## 5.考虑本地网络技术

正如我在我的[裸体水疗博客系列](https://medium.com/cto-as-a-service/the-naked-spa-part-i-96980aa1e9f9)中广泛讨论的那样，在过去的 20 年里，网络已经缓慢但稳定地演变成一套非常强大的基础技术，值得投资。例如，如果您在 15 年前学习了 JavaScript，那么跟上时代并应用当前的最佳实践并不困难。例如，ES6、Web 组件、async/await 和代理类将标准浏览器技术带到了新的高度。所以，如果我们抛开一些关于*无框架*网络开发的神话？

1.  **香草 JavaScript 只针对小项目**
    完全同意。ECMAScript 已经发展了。我们不是在谈论窗口范围的垃圾和内联点击处理程序。尽情发挥，了解原生 ES6+的功能。
2.  使用普通的 JavaScript 就像重新发明轮子一样
    框架可能看起来有很多现成的功能，那么为什么要用纯 JavaScript 重写呢？答案是:框架经常会重新发明轮子，或者强制执行一些不符合 web 发展状态的非本机工作方式。你可以用本地网络技术做任何事情。对此的证明在于框架实际上在幕后使用它。
3.  **没有路由器、SPA 功能、反应式数据绑定等…**
    使用原生 ES6+这一切其实相当容易。只是让你自己熟悉它，使用伟大的资源，如[vanilla.js.org](http://vanilla.js.org/)、[gomakethings.com](http://gomakethings.com/)、[vanillajstoolkit.com](http://vanillajstoolkit.com/)或 [xo-js.dev](https://www.xo-js.dev/) (其中包括一个 [SPA 路由器](/a-spa-pwa-router-in-pure-vanilla-es6-javascript-e8f79cfd0111))。另外，请看下面的文献部分以获取灵感。

最重要的是，你应该庆幸框架的重量刚刚从你的肩膀上落下。我见过相对简单的 Angular 应用程序携带 6MB(！)的下载。我们都知道页面/应用的速度会影响 SEO，并且会对转化率产生负面影响。

# 文学

*   前端框架是解决方案还是臃肿的问题？| Toptal
*   【TimKadlec.com Javascript 框架的成本——网络性能咨询| 
*   [过度投资 JavaScript 框架的成本——开发社区](https://dev.to/ryansmith/the-cost-of-investing-too-heavily-in-a-javascript-framework-2121)
*   [3 种主要的技术债务以及如何管理它们| HackerNoon](https://hackernoon.com/there-are-3-main-types-of-technical-debt-heres-how-to-manage-them-4a3328a4c50c)
*   [投资正确的技术以避免技术债务——开发社区](https://dev.to/sunnysingh/investing-in-the-right-technologies-to-avoid-technical-debt-2c06)
*   [纯普通 ES6 JavaScript 的 SPA/PWA 路由器| Marc van neer ven |用简单英语编写的 JavaScript](/a-spa-pwa-router-in-pure-vanilla-es6-javascript-e8f79cfd0111)

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***

## 进一步阅读

[](/bad-documentation-is-tech-debt-heres-how-you-solve-it-ce1d0b3ee760) [## 糟糕的文档是技术债务——以下是解决方法

### 如果你想快速行动，尽可能少破坏东西，文档文化是至关重要的，那么为什么好的文档…

javascript.plainenglish.io](/bad-documentation-is-tech-debt-heres-how-you-solve-it-ce1d0b3ee760)