# React 项目失败的故事

> 原文：<https://javascript.plainenglish.io/story-of-a-failed-react-project-f32177479bdf?source=collection_archive---------0----------------------->

## 这给我们的创业带来了灾难。

![](img/138721aa3f35a539b822704207eb2ad3.png)

Photo by [Andrea Piacquadio](https://www.pexels.com/@olly?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/desperate-evicted-male-entrepreneur-standing-near-window-3771129/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

一个项目是如何失败的？你怎么知道你现在正在做的项目是注定要失败的呢？

这不是一个容易回答的问题，但我们可以尝试剖析一个已经失败的项目，以获得更好的画面。

这就是我今天要做的。

# 为什么？

在之前的一个故事中，我分享了[我们的创业如何失败](https://medium.com/p/fe270158ed0b)。这背后的一个主要原因是技术故障。

由于我从一开始就参与了开发过程，我亲眼目睹了这一切是如何失控的。

对我来说，这不是一个值得骄傲的故事，但我可以肯定地说，这次经历造就了今天的我。我也将分享这个转变的故事。

# 我们避免最佳实践。

对于开发者来说，有大量的原则。[扎实原则](https://betterprogramming.pub/how-to-apply-solid-principles-to-clean-your-code-in-react-cdfd5e0a9cea)、[干原则](/5-dry-principles-to-follow-in-react-6ca0405986a9)、[干净编码](https://medium.com/p/df788a682fb)等就是其中最值得注意的一些。但作为大三学生，我们有时会陷入成绩陷阱。

构建人们可以使用的东西成为我们开发者的一个骄傲点。事实上，这正是我们在做在线课程时被告知的。

我们很少关心项目的内部架构，更不用说遵循最佳实践了。我们只是添加了一些功能，却什么也没做。

# 但是要求变了

我仍然记得我们的大部分组件都在 500 线以上。真是一团糟。但不幸的是，我们当时无法理解。因为我们过于关注运输功能，以至于忽略了大局。

然而，当我们开始获得客户反馈时，事情开始引起问题。碰巧的是，我们一开始假设的许多事情都是错误的，我们不得不从头开始。

每一个微小的修改要么破坏了其他东西，要么需要完全重写组件，这需要更多的测试，一些其他部分会失败，等等。

你明白了。

# Git 使用不当

Git 和 Github 对我们来说很容易上手。但我们只是用它来在线存储代码，没有其他用途。比如

*   维护有意义的分支机构名称。
*   问题跟踪
*   释放管道
*   磨尖

我们从来没想过这些。

我们研究以我们名字命名的分支。是的，所以我工作的部门被命名为费萨尔。

我们对我们的东西进行编码，然后把它和母版融合在一起。就是这样。我知道这听起来很奇怪，但那时候就是这样。

结果我们太害怕了，什么都不敢删。

在某一点上，我们开始命名我们的组件，如 **SampleComponent.jsx** 和 **SampleComponentNew.jsx** 。害怕丢失一些我们将来可能需要的代码！

您可以理解随着时间的推移，这些事情是如何累积起来产生大量技术债务的。

没有在正确使用 git 上投入足够的时间，代价会超出人们的想象。

# 缺乏经验的开发人员

我们只是大学生活结束时的一帮朋友。而且我们雇的人也很没有经验。

这背后有两个原因。低年级学生雇佣起来很便宜，他们并不比我们懂得多。

我们有一种自我满足感，因为我们已经有所成就。结果，当我们意识到自己的一些错误时，已经太晚了。

**因为文化已经很糟糕了，我们就是走不出来。**

# 不是测试

是的。我想这是显而易见的。

我们通过测试可以获得的主要好处是减少了手动测试的时间，手动测试需要在每次改变后进行，这浪费了很多时间。

即使是现在，在这个行业工作了几年之后，我还没有看到一个项目的测试是正确完成的。

这并不是说 100%的覆盖率是正确的方法，但是至少一些像 [react-testing-library](https://testing-library.com/docs/react-testing-library/intro/) 和 [cypress](https://www.cypress.io/) 这样的功能测试可以节省很多时间。

# 没有尽早利用 TypeScript。

那时，TypeScript 越来越受欢迎。我们最终采纳了它，但为时已晚。

事实上，当我们开始添加 TypeScript 时，我们意识到我们必须重写整个内容。

我可能不需要解释为什么 TypeScript 很重要，但是回过头来看，我可以看到更早地采用 TypeScript 如何能够更好地帮助我们。

# 我学到了什么？

嗯，很多事情。事实上，我的 Medium profile 是一个生活日志，记录了我一路走来学到的东西。

## 最佳实践

最佳实践的出现是有原因的。我学会了在给变量和函数命名时更加小心，让事情变得小而整洁。

[](https://betterprogramming.pub/21-best-practices-for-a-clean-react-project-df788a682fb) [## 清洁 React 项目的 21 个最佳实践

### 提高代码质量的实用建议

better 编程. pub](https://betterprogramming.pub/21-best-practices-for-a-clean-react-project-df788a682fb) 

## 设计原则

像 SOLID ann DRY 这样的设计原则可以帮助您在日常基础上决定何时做出技术选择。

我学会了为什么它们是必不可少的，以及如何有效地使用它们。

[](https://betterprogramming.pub/how-to-apply-solid-principles-to-clean-your-code-in-react-cdfd5e0a9cea) [## 如何在 React 中应用坚实的原则来清理代码

### 审视单一责任原则在实践中的运用

better 编程. pub](https://betterprogramming.pub/how-to-apply-solid-principles-to-clean-your-code-in-react-cdfd5e0a9cea) [](/5-dry-principles-to-follow-in-react-6ca0405986a9) [## 反应中要遵循的 5 条干燥原则

### 今天你可以使用的 5 个有用的技巧！

javascript.plainenglish.io](/5-dry-principles-to-follow-in-react-6ca0405986a9) 

## 正确使用 Git

我学会了如何高效地使用 Git 和 GitHub。我仍在学习它，每天都被它的深度所吸引。

我了解到有效的发布管道机制可以帮助消除许多令人头痛的问题。

[](/continuous-deployment-pipeline-for-react-apps-886f887996f8) [## React 应用的持续部署渠道

### 使用 Github 操作和 AWS S3

javascript.plainenglish.io](/continuous-deployment-pipeline-for-react-apps-886f887996f8) 

## 测试

我忽略了这么长时间！但现在我知道了它的重要性，也数不清它救了我多少次 a**。

[](https://betterprogramming.pub/everything-you-need-to-get-started-with-testing-in-react-e16819b0eba7) [## 在 React 中开始测试所需的一切

### 给初学者的简明介绍

better 编程. pub](https://betterprogramming.pub/everything-you-need-to-get-started-with-testing-in-react-e16819b0eba7) 

## 我变得节俭了

我艰难地认识到为正确的工作选择正确的工具的重要性。我不会说我已经变得完美，但在选择任何图书馆之前，我会花大量的时间研究图书馆内外，以做出明智的决定。

[](/45-npm-packages-to-solve-16-react-problems-a9ab18946224) [## 45 个 NPM 软件包解决 16 个 React 问题

### 关于如何选择完美的 npm 包的深入指导

javascript.plainenglish.io](/45-npm-packages-to-solve-16-react-problems-a9ab18946224) 

这就是我的故事。希望这个故事能帮助你下次做出比我更好的决定。有的边做边学；其他人可以通过看别人失败来学习。

我希望你能从这个故事中学到一些东西。

非常感谢您阅读全文。

祝您愉快！

**有话要说？通过**[**LinkedIn**与我联系](https://www.linkedin.com/in/56faisal/)

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*

[](/20-essential-parts-of-any-large-scale-react-app-ee4bd35436a0) [## 任何大型 React 应用程序的 20 个基本部分

### 如果您正在编写企业级代码，您需要了解这一点

javascript.plainenglish.io](/20-essential-parts-of-any-large-scale-react-app-ee4bd35436a0) [](https://betterprogramming.pub/22-best-practices-to-take-your-api-design-skills-to-the-next-level-65569b200b9) [## 22 个最佳实践，让您的 API 设计技能更上一层楼

### 设计 REST APIs 的实用建议

better 编程. pub](https://betterprogramming.pub/22-best-practices-to-take-your-api-design-skills-to-the-next-level-65569b200b9)