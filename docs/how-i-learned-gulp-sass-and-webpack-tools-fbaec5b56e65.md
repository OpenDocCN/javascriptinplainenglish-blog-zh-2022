# 我如何学习 Gulp、Sass 和 WebPack 工具

> 原文：<https://javascript.plainenglish.io/how-i-learned-gulp-sass-and-webpack-tools-fbaec5b56e65?source=collection_archive---------16----------------------->

## 我自己使用的有价值的学习材料。

![](img/2ff38987359fb3c5ba1629cd5f54a1c8.png)

Photo by [Dmitry Ratushny](https://unsplash.com/@ratushny?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

前端开发人员的工作基础是 HTML、CSS 和 JavaScript。这并不意味着掌握了它们之后，学习就结束了。有很多工具可以让你的工作变得更容易，没有它们，项目实际上是不可能的。

今天，每个想探索 web 开发秘密的人都应该知道其中的三个。

我推荐我自己用的有价值的学习资料。这篇文章很长，但是我试图收集材料来很好地解释每一个被描述的工具。因此，您可以将本文作为学习 Sass、Gulp 和 Webpack 的起点。

这些工具在某种程度上是相关的。但是关于它的细节。开始吧！

# 厚颜无耻

什么是萨斯？它是一个 CSS 预处理器，使得设计网站或应用程序更加容易。

由于引入了嵌套、变量或所谓的 mixins，它避免了重复代码，使处理样式更加直观。

我们当中有谁不想创建一个带有颜色名称的变量，而不是不断地键入它的代码呢？萨斯让我们有可能。这只是它的众多功能之一。自从认识了萨斯，我真的不再用纯 CSS 了。

我推荐你从[官网](http://sass-lang.com/)开始学 Sass。当然，值得特别关注的是[文档](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)，它并不太长，并且确实很好地解释了功能。

如果你更喜欢以课程的形式了解萨斯，我建议你先去 Codecademy 的[课程。它可以让你学习基础知识，了解 Sass 是怎么回事。Codecademy 课程的缺点是它没有解释如何安装 Sass 并在您的项目中使用它。](https://www.codecademy.com/learn/learn-sass)

不幸的是，事实并非如此，你只需要输入代码，它马上就能工作。Sass 是一个预处理器，它需要将 scss 文件转换成 css 文件，为此我们需要特定的工具(在这篇文章的后面会详细介绍)。

另一个我推荐的课程是 CodeSchool 的 [*汇编 Sass*](https://www.codeschool.com/courses/assembling-sass) 。进入该系统是免费的，课程的其余部分对购买了该网站访问权限的人开放。

这个课程并不是很有启发性，所以我认为不值得仅仅为了它而购买 CodeSchool 的访问权限。但是如果你有门路的话，还是值得去上这门课的。

# 吞咽

今天接下来是大口。在前端开发人员的工作中，它是一个非常重要的工具，因为它允许您自动化许多任务。

多亏了我们有了配置的可能性，你可以为自己节省很多时间。Gulp incl 编译 Sass 文件，刷新浏览器页面(当我们在编辑器中保存更改时，由于这一点，我们可以立即看到我们的页面如何更改)，合并文件(例如，在项目中，我们可以将许多 scss 文件合并为一个 css 文件)或添加适合不同浏览器的前缀(当我们需要在其他浏览器中指定给定功能时)。当然，这还不是全部。

听起来很棒，对吧？起初，这对我来说有点神奇。

然后，我发现当你想使用 Gulp 时，首先要知道的是 Node.JS，这是一个不使用浏览器运行 JavaScript 的环境。

关于如何安装节点的说明。当然，JS 可以在他们的网站上找到。一旦我们有了节点。JS，我们可以使用 NPM，这是节点包管理器。他将为我们的项目安装适当的包，包括与 Gulp 的包。

我们从控制台级别使用 Npm，这使得项目工作更加容易。我们不必手动进入目录来安装或解压软件包。我们使用在控制台中输入的各种命令来做所有事情。

安装节点后。JS 和 NPM，我们可以通过控制台安装 Gulp。你可以在 GitHub 上的[Gulp 资源库中了解如何做。](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)

当然，安装是一回事，使用又是另一回事，你得学会如何高效地使用 Gulp。

首先，我向初学者推荐 CSS-tricks 网站上的[](https://css-tricks.com/gulp-for-beginners/)*文章。它不仅解释了如何安装 Gulp，还解释了如何配置您的第一个文件以及如何在您的项目中使用它。*

*也可以参考[官方 Gulp 网站](http://gulpjs.com/)。不过，在这种情况下，我首先没有参考文档，因为上面提到的文章解释得更清楚。*

# *网络包*

*这是另一个工具，它极大地改善了使用 HTML、CSS 和 JS 构建的应用程序或网站的工作。Webpack 是所谓的*模块捆绑器*，它允许我们创建分成许多模块的代码，Webpack 随后将这些模块组合起来。*

*这听起来可能有点神秘，但你可以很快明白它是什么。Webpack 处理应用程序并创建依赖图(或树)。*

*也就是说，它构建一个应用程序，并根据它确定的依赖关系安排文件的加载顺序。检查哪个文件必须导入到另一个文件中，等等。*

*定义所谓的*入口点*是很重要的，这样 Webpack 就知道哪个是根文件，依赖项应该从哪里开始。如果您对解释 Webpack 如何工作的更多说明性示例感兴趣，请参考 Webpack 官方网站上的 [*Webpack 教程*](https://medium.com/ag-grid/webpack-tutorial-understanding-how-it-works-f73dfa164f01) 文章和 [*概念*](https://webpack.js.org/concepts/) 部分。*

*这些工具使处理代码变得更加容易和愉快。花时间熟悉这些工具是值得的，因为作为前端开发人员，每天都会用到它们。*

*尽管我们经常为 Gulp 或 Webpack 配置适当的文件，但我们不必从头开始创建它们。有必要了解它是如何工作的，以及如果有必要，我们可以如何轻松地改变或更新某些东西。*

**更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。****