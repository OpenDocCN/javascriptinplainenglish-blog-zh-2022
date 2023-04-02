# 层优先还是特征优先:一个好的颤振项目结构如何获得回报

> 原文：<https://javascript.plainenglish.io/layer-first-or-feature-first-how-a-good-flutter-project-structure-pays-off-b0e7d901c0cd?source=collection_archive---------1----------------------->

![](img/2cda71e98f41cf41edd297162e18c372.png)

Image by: Milan Source: Self create

Flutter 是 Google 的一个高级移动开发框架。它是在 Android 和 iOS 设备上创建高质量用户界面的绝佳选择。然而，为了从 Flutter 中获得最大收益，正确构建项目是至关重要的。

因为开发可能看起来很有趣，有时候跟踪你的应用程序在代码中的位置并不容易。当你有太多的代码时，很难找到合适的代码来修复一个错误或者实现一个新特性。也很难找到合适的文件来存储一个概念或想法。感觉就像你淹没在代码的海洋中。

因此，当开始一个 Flutter 项目时，组织你的代码使其易于阅读和理解是很重要的。在创建 Flutter 项目时，您应该注意项目结构的几个关键方面。最重要的是你的文件和文件夹的组织。以合理的方式组织文件和文件夹至关重要，以便在需要时可以轻松找到它们。

但是如果你没有呢？在你的 Flutter 项目中缺少合适的文件或文件夹结构会导致项目增长时出现许多棘手的问题。例如:

在存储库中定位特定文件将变得困难且耗时；

会给团队合作带来问题；

会增加项目维护的难度；

维护一个 Flutter app 的成本更高；

创建新的或删除无用的功能成为开发人员的噩梦；

在最坏的情况下，它可能会导致应用程序性能不佳。

所以，如果你不想在后端制造混乱，你应该采用合适的方法 [**来构建你的颤振项目**](https://kodytechnolab.com//blog/layer-first-or-feature-first-flutter-project-structure/) 。本文档描述了两种有效构建项目的最佳实践。让我们逐一探索。

**第一层**

众所周知，应用架构由四层组成，每层都包含应用的基本组件。

演示:状态、小部件和控制器

应用:服务

领域:模型

数据:数据源、存储库和数据传输对象——dto

因此，当您采用层优先的方法时，不要将 Dart 文件放在层内；相反，您可以在每个图层中创建特征文件夹。然后，将所有 Dart 文件添加到您创建的适当的特征文件夹中。因此，它也被称为层内特征。假设我们在项目中有一个特性，那么层优先的结构应该是这样的:

‣自由报

‣ src

‣演示

‣特色 1

‣应用

‣特色 1

‣领域

‣特色 1

‣数据

‣特色 1

**2 功能优先**

与第一种方法相比，特征优先集中在特征上，并在每个特征内进行分层。这四个图层保持不变，但它们的位置现在位于每个要素内部。使用与上面相同的示例，特征优先结构将如下所示:

‣自由报

‣ src

‣特色

‣特色 1

‣演示

‣应用

‣领域

‣数据

‣特色 2

‣演示

‣应用

‣领域

‣数据

我们使用了两个特性来给你一个清晰的概念。现在，您可以根据需要添加任意数量的要素，并在其中创建图层。

如果你对选择哪种方法感到困惑，你可以咨询一下 [**颤振专家**](https://kodytechnolab.com/hire-flutter-app-developer) 。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*