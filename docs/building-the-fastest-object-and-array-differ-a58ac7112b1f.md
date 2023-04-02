# 构建最快的对象和阵列不同

> 原文：<https://javascript.plainenglish.io/building-the-fastest-object-and-array-differ-a58ac7112b1f?source=collection_archive---------7----------------------->

![](img/eb41cf25edf36615bf10ff94c0f0f097.png)

Microdiff’s logo

## 我如何构建 Microdiff，以及它如何比大多数其他对象和数组差异库更快

我维护 [Microdiff](https://github.com/AsyncBanana/microdiff) ，这是一个性能和大小优化的库，用于深度对象区分。有人在一期[微 diff](https://github.com/AsyncBanana/microdiff/issues/2#issuecomment-962491393)中发帖，要求我写一篇关于我如何快速制作微 diff 的博文。

> *我相信一个解释者(也许是一篇博文？)您注意到的其他库的低效率以及您如何克服它们(包括您所说的不受支持的“边缘情况”)将会非常有趣。它们还有助于正确解释基准测试的结果。*

所以，我决定这么做。这篇博文描述了我如何使 Microdiff 比大多数其他对象和数组 diffing 库更快。

> ***免责声明*** *:我对这个题目很有偏见。*

# 差异简介

Diffing(差异跟踪)是跟踪两个对象之间的不同之处。例如，假设你有两个对象，对象 a 和对象 b。

使用 Microdiff，要获得差异，您可以这样做:

如您所见，所有的更改，无论是值的更改、添加还是删除，都被记录了下来。差异对于许多事情来说是必不可少的，比如虚拟 DOM，因为它们需要记录元素的变化。现在，让我们来了解一下微 diff 之前的 diffing 生态系统的问题。

# 微观分化前的分化生态系统

不同的生态系统处于一种糟糕的状态。许多图书馆下载了数百万次，但没有得到积极维护，而且制作质量很差。现在，让我们看看第一个例子，deep-diff。

## 深度差异

Deep-Diff 是用于深度对象区分的最流行的 JavaScript 库之一。它每周获得 100 万到 200 万次下载，拥有超过 10k 颗 GitHub 星的工具都在使用它。

然而，它有许多缺陷。首先，最后一次提交是在 2019 年，它没有遵循现代的约定，如支持 ESM 和提供捆绑的 TypeScript 类型。

此外，它的尺寸和性能也有问题。它的大小为 5.5kb，压缩后为 1.9kb。这个大小并不可怕，只是这是一个简单的实用程序，因此应该有一个更小的大小。相比之下，Microdiff 的大小为 0.9kb minified 和 0.5kb Gzipped。

现在，就性能而言，Deep-Diff 也做得不好。它不能做得很小或很快，因为它有许多不同的功能，这增加了大量的开销。此外，它不做诸如分组类型行为之类的事情来提高性能。因为所有这些事情，Microdiff 可以比[快 400%](https://github.com/AsyncBanana/microdiff#benchmarks)。

## 深层对象差异

[Deep-Object-Diff](https://www.npmjs.com/package/deep-object-diff) 是另一个流行的 diffing 库。虽然它自 2018 年以来一直没有更新，但它拥有 Deep-Diff 所缺少的一些现代功能，如 ESM 和内置的 TypeScript 类型。

此外，如果使用基本差分，它可以以接近微 diff 的速度运行。然而，它仍然有两个问题，大小和它提供的信息。

首先，虽然它没有 deep-diff 大，但仍然很重要，5.2kb minified 和 1kb Gzipped。其次，由于输出的设计方式，它提供的细节很少。

在微 diff 提供变更类型、新值、旧值和路径的情况下，Deep-Object-Diff 的最详细的 diff ( `detailedDiff`)不提供旧值。此外，如果您想要接近微 diff 速度，您必须使用主 diff 函数而不是`detailedDiff`，这样您就不知道变化类型。

## JSDiff

虽然 JSDiff 支持对象区分，但它主要是为区分文本而设计的。它很大，有 15.8kb 的 Microdiff 和 5.9kb 的 gzip，而且非常慢(比 Microdiff 慢 2100%)。我不会深入解释为什么它这么慢，因为它根本不是为对象区分而设计的。

# Microdiff 如何解决这个问题

## 注重性能的架构

Microdiff 通过专注于性能和大小而不牺牲易用性，解决了许多这样的问题。它不是一个复杂的函数网络，而是一个简单的递归函数。Microdiff 还使用类似组合类型行为的策略来减小大小，同时提高性能。

例如，假设您想要查看 RegEx 和 JavaScript 日期之间的差异。为了获得准确的变更跟踪，您必须将 RegEx 字符串化，并将日期转换成数字。一个简单的实现可能是这样的:

这是可行的，但是如果您也需要检查`new String()`对象或`new Number()`对象呢？(`new String()`和`new Number()`不创建原语，所以你必须将它们转换成类似于日期和正则表达式的原语)为了解决这个问题而不引入大量的`if then`，Microdiff 的实现是这样的:

这段代码首先得到一个不能直接比较的类型列表(`richTypes`)。

然后，它检查该值是否属于这些类型之一。如果是，那么代码检查该值是否可以用`isNaN`强制转换成一个数字。如果可以的话(在日期和`new Number()` s 的情况下是真的)，它检查被强制为数字的版本。如果不是(RegEx 和`new String()`就是这种情况)，它将值强制转换成一个字符串，并比较该版本。

在 Microdiff 中，实际的 rich 类型转换逻辑并没有太大的不同，尽管有一些差异减小了大小，并有助于逻辑与代码的其余部分相适应。

诸如此类的事情是 Microdiff 速度快的部分原因。然而，另一个原因是它只关注更常见的情况，而不是每一种可能的边缘情况。

## 关注 99%的案例，而不是解决所有边缘案例

在这方面，Microdiff 自发布以来已经有了很大的改进。事实上，自从编写了[初始解释](https://github.com/AsyncBanana/microdiff/issues/2#issuecomment-960291469)以来，Microdiff 已经增加了对更丰富类型和循环引用的支持。

然而，仍有一些情况下，Microdiff 的行为不太正确，比如在比较具有原型属性的对象时，因为它包含了原型属性。类型组合为列出的类型解决了这个问题，但不是为所有其他类型。

在以前的测试中，排除原型属性的方法并不快速。但是，我可能会为您添加一种方法来为字符串/数字强制传递自定义继承类型，这可能对某些事情有所帮助。然而，目前这是不可能的。

# 结论

总之，Microdiff 是速度最快的区别库，因为它以性能为中心的体系结构和对 99%案例的关注，并且 Microdiff 仍然能够使用现代功能，使其易于使用。如果你对 Microdiff 感兴趣，请查看 GitHub repo 。希望你从中有所收获，感谢你的阅读。

*最初发表于 2022 年 1 月 1 日*[*【https://byteofdev.com】*](https://byteofdev.com/posts/microdiff/)*。*

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***