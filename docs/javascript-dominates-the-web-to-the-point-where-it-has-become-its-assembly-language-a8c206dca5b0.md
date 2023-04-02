# JavaScript 主宰着网络，已经成为了它的汇编语言

> 原文：<https://javascript.plainenglish.io/javascript-dominates-the-web-to-the-point-where-it-has-become-its-assembly-language-a8c206dca5b0?source=collection_archive---------8----------------------->

## 它还会是无可争议的网络语言吗？

![](img/756727108790476b15fd5354ef572c4b.png)

Photo by [Jackson So](https://unsplash.com/@jacksonsophat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我们想到 web 开发时，我们会想到 HTML 标签、CSS 样式表，尤其是 JavaScript 编程语言。后者主宰了网络，以至于成为了它的汇编语言。全球 93.1%的网站是用 JavaScript 编写的，它在开发者中的受欢迎程度持续增长。年复一年，我们看到新书、新教程、新工作、新追随者、新图书馆、新网站和新代码。

但是它的未来呢？它还会是无可争议的网络语言吗？它会继续统治所有软件吗？

问这些问题似乎很荒谬，因为答案似乎显而易见。但是，在回答这个问题之前，让我们先分析一下 JavaScript 及其生态系统背后的信号，从最近的开始。

## **JavaScript，web 客户端**

2016 年 2 月，谷歌发布了一项重要的网络公告。对于移动网站的出版商来说，要想从其新的 AMP(加速移动网页)技术中受益，他们必须减少或消除代码中的 JavaScript。对谷歌来说，信号很清楚:JavaScript 在移动网络上缺乏性能。

2015 年 6 月，谷歌、苹果、微软和 Mozilla 合作发布了 WebAssembly，这是一种字节码，主要目标是最终取代 JavaScript。

Chrome、Safari、Edge 和 Firefox 背后的设计者已经在尝试从 C 和 C++语言中生成这种字节码。

回想一下，直到现在，这些语言主要用于系统编程。一旦这些实验结束，如果字节码成为标准，其他传统语言如 Java 和 C#很可能会走上成为 web 语言的道路。JavaScript 将不再是唯一的主宰。

但这两项举措并不新鲜。其他人以前也出现过。的确，自 1995 年 5 月诞生以来，我们就开始看到方言。最受欢迎的是 CoffeeScript 和 TypeScript，coffee script 是由前《纽约时报》平面设计师在 2009 年设计的，TypeScript 是由微软的一个工程师团队在 2012 年创建的。

除了这些方言，我们还开始看到越来越多的 transpilers，这种翻译器允许任何人用传统语言开发并生成可以在浏览器中运行的 JavaScript 代码。

迄今为止，我们有 200 多种方言和 transpilers。有些提供 C、C++或 Java 语言，有些提供 Python、Ruby 或 Erlang 语言，但是 JavaScript 生态系统并不局限于这些方言和 transpilers。

它也由 27 个“框架”组成，其中最著名的是 jQuery、Bootstrap、Backbone.js 和 AngularJS。并且这些扩展的列表越来越多。要认识到这一点，你必须定期查阅 GitHub 平台，它已经成为自由软件的最大市场。

乍一看，这种丰富性似乎是 JavaScript 语言及其不断发展的生态系统的优势。但是，如果我们分析所有这些方言、所有这些 transpilers 和所有这些“框架”发展背后的原因，我们会发现两个重大的局限性:初始语言的语法和性能。

对于一些设计师来说，尤其是那些习惯于 Python、Ruby 和 Haskell 等编程语言的设计师，JavaScript 考虑不周，设计得太快。

对于其他人，尤其是那些习惯于 C、C++和 Java 等编程语言的人来说，JavaScript 成为生产语言的速度很慢。对所有人来说，语言必须改进，这是网络上这种激增的起点。

有一个围绕编程语言的大型社区是令人放心的。尽管如此，最好是有一个明确的发展愿景，而不是在没有战略的情况下向各个方向扩散。

JavaScript 有太多的方言、太多的 transpilers 和太多的“框架”，这些最初是一个优势，但已经成为该语言未来的一个问题。

最初的设计是为了扩展它的功能或纠正它的一些缺点，但它们有时会提供不兼容的解决方案。选择一种方言、一个 transpiler 或一个“框架”已经成为一场赌博，因为你不知道你所选择的技术是会长期保持下去，还是会在短时间内被一种更时髦的新技术所抛弃。

事实上，自由软件给你提供了自由访问的机会，但是它不能保证你的连续性。在 GitHub 上，你可以找到质量优秀的高级软件和实验库，往往不完整。

为了保持作为网络参考语言的地位，JavaScript 需要一种用户友好、高效、高质量的方言，以支持大规模网站的开发。TypeScript 可能就是那种方言。它得到了微软的支持，最近被谷歌用于其 AngularJS 2.0 框架。此外，它遵循 ECMAScript 标准的规范，ECMAScript 标准管理着 JavaScript 语言的发展。

## **JavaScript，超越 web 客户端**

如果我们离开客户端，分析 JavaScript 在服务器端的存在，情况就清楚多了。Web 服务器是 PHP 和 ASP 的领域，分别装备了全球 81.9%和 15.7%的网站。由于其服务器端 NodeJS 版本，JavaScript 出现了，但只有 0.2%的网站，远远落后于 PHP 和 ASP.NET。

如果情况发生变化，一个新的参与者可能是谷歌在 2009 年开发的 Go 语言，以取代其高性能服务器中的 C、C++和 Java 语言。

当我们进一步深入到应用层时，我们主要会发现 Java、C#、C++和 C。这些是管理商业公司、公共行政部门和非商业组织的内部系统的语言:ERP、CRM、HR、电子商务、BI 和所有事务性应用程序。

由于缺乏性能和系统功能支持，JavaScript 或 NodeJS 没有理由成为应用程序级别的高级语言。如果有一种新语言能在这一层找到一席之地，那就是 Go，因为它在性能上更接近 C 和 C++，而且更适合需要应用层的大型系统和大型网络。

当我们进一步深入到数据层时，我们进入了由数学和统计学语言(如 R、Matlab、Octave 和 Python)管理的数据分析和机器学习世界。

JavaScript 爱好者正试图开发科学计算扩展来进入这一层，但 JavaScript 的 DNA 中没有数据分析和机器学习。这里唯一的新成员可能是 Julia 语言，它是麻省理工学院在 2009 年设计的，用来取代 R、Matlab、Octave 和 Python。

后者缺乏性能，主要用于原型的开发阶段，原型一旦稳定，就必须在投入生产之前用 Fortran、C 或 C++进行记录。

Julia 可以改变 R&D 团队目前在设计原型的“数据科学家”和将这些原型转化为生产系统的计算机科学家之间的分工。有了朱莉娅，就不需要这种分工了。

## **移动和云时代的 JavaScript**

随着 web 客户端越来越移动，web 服务器越来越基于云，适应这种新计算模型的编程语言的前景正在发生变化。这给新语言提供了替代现有语言的机会。

Go 可能成为 Java 的替代品，Java 目前是在 Android 上开发应用程序的事实上的标准。同样，苹果在 2014 年设计的语言 Swift 可能会取代 Objective-C 成为 iOS 的编程语言。

无论是 Java 还是 Objective-C 继续统治移动网络，还是让位于 Go 和 Swift，有一点是肯定的:JavaScript 不会是统治移动网络的唯一语言，尤其是自从 GoogleAMP 推出以来。

然而，JavaScript 不会在一夜之间消失。这个故事表明，编程语言要么像 C++和 Java 一样进化，要么像 Cobol 和 Pascal 一样停滞或衰落。这些年来，JavaScript 发生了很大的变化，通过 ECMAScript 规范，语言本身也发生了变化。

## **让我们看看不久的将来会向我们展示什么。**

编程语言的世界是动态的。每一代新技术都会带来新的语言或新的用途。谁会想到手机和“云”会把一台超级计算机放进我们的口袋？

这要归功于一代又一代互不相同的编程语言。JavaScript 是其中之一，但不是最后一个。新的语言链将继续带给我们新的惊喜。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*