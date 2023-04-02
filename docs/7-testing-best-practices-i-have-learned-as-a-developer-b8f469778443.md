# 7 测试我作为开发人员学到的最佳实践

> 原文：<https://javascript.plainenglish.io/7-testing-best-practices-i-have-learned-as-a-developer-b8f469778443?source=collection_archive---------10----------------------->

## 超过 4 年的开发经验

![](img/2b69d4dfad1182ac25ffe52eda9afeb6.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我不是一个经验丰富的开发人员，我承认我有很多东西要学习。但是在这篇文章中，我想分享一些我从测试最佳实践中学到的东西。

谁知道呢，也许一年后我看到这个会笑。或者更糟，因为我没有跟随他们而惩罚我。

# 普遍原理

所有的测试都应该类似于我们的组件或屏幕的工作方式。它们越像这种行为，我们对它们的使用就越有信心。

实现这一点的最佳方式是不要像开发人员那样思考。而是像用户一样思考。

# 最佳实践

1.  **测试应该是可读的**
    测试揭示了组件/屏幕及其逻辑工作的方式。因此测试应该是可读的，因为可读的测试允许(甚至)新开发人员看一眼就能理解。
2.  **避免相互依赖
    这是什么意思😕？嗯，当编写多个测试时，你应该能够以任何顺序编写和运行测试，并且它们应该仍然通过。**
3.  **永远，永远，永远避免在测试中写逻辑** 只关注动作和动作的预期结果。如果您需要编写逻辑来使您的测试通过，那么您的代码的实现就是错误的。
4.  **不要在一个测试中有太多的断言(尤其是当你不需要它们的时候)** 最有效的测试是一次测试一个用例。如果您需要在一个测试中有多个断言，那么可以考虑将这个测试分成多个测试套件。
5.  **硬编码测试值，如果你需要的话** 将你的测试与实现值混合在一起会使测试变得无用，并导致测试失败。在日历组件中可以看到这样的例子，其中硬编码的值用于测试最初的月份。如果使用实现值，那么每个月都必须编写一个新的测试，这不是很有效。
6.  **在开发时编写测试，而不是在完成实现之后** 这是 TDD(测试驱动开发),它很有用，因为尽早编写测试有助于编写更好/更干净的代码，并快速消除 bug。在最后编写测试可能会让人不知所措，尤其是如果有许多实例要测试的话，并且还会导致在测试覆盖期间分支的某些部分没有被覆盖。
7.  需要时更新测试
    代码库就像一个活的有机体。它会成长和变化，所以维护测试是测试的一个重要部分。
    如果在一个已经创建的组件的扩展功能上工作，并且该组件已经有测试，那么更新规范文件将会导致更大的覆盖范围，并且对于任何其他想要在将来了解该功能的行为的开发人员来说，这将是一个有用的文档。

目前就这些。随着我了解更多，我会更新这个列表。您认为我应该添加什么最佳实践吗？

如果这是有帮助的，如果你给这篇文章一个👏如果你还没有，关注一下会很好。

也请考虑通过下面我的[推荐](https://mazaher-muraj.medium.com/membership)链接订阅 Medium。这很棒，我用它来了解技术领域的最新动态，并从其他开发人员的经验中学习。

你的订阅将直接支持我和许多其他媒体作家。

[](https://mazaher-muraj.medium.com/membership) [## 通过我的推荐链接加入媒体

### 阅读 Mazaher Muraj(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

mazaher-muraj.medium.com](https://mazaher-muraj.medium.com/membership) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。**