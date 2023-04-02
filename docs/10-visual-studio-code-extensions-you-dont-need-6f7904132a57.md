# 您不需要的 11 个 Visual Studio 代码扩展

> 原文：<https://javascript.plainenglish.io/10-visual-studio-code-extensions-you-dont-need-6f7904132a57?source=collection_archive---------0----------------------->

## Visual Studio 代码

## 这些流行的扩展解决了不存在的问题

![](img/d7e576f2b1f0f8554e8a51b1a4c97724.png)

Photo by [Daryl Wilkerson Jr](https://www.pexels.com/photo/stop-sign-2387708/)

最近，我决定对我的 VS 代码设置进行一次批判性的审视，并在我的工作流程中寻找改进，去掉不再使用的扩展。我发现我安装了一堆不需要或不再需要的扩展。

由于扩展可能会导致性能问题，增加 CPU 的使用，并且可能会与其他扩展或本机功能发生冲突，所以最好将扩展限制在您需要的范围内。

最让我震惊的是，在 Medium、dev.to、Reddit 和其他平台上仍然有帖子推荐这些扩展，尽管其中一些在下载页面的顶部有明确的反对通知。

## 如何编辑设置

在我们浏览扩展列表之前，最好提一下这些扩展中有许多是 Visual Studio 代码中固有的。您可以通过设置菜单启用/禁用或控制这些功能的行为。

可以通过 UI 或 JSON 配置来控制设置，出于本文的目的，我们将使用 JSON 版本，因为从这里复制要简单得多。

您可以通过命令调板(⇧⌘P).)打开 settings.json 来设置您的全局 Visual Studio 代码输入设置，选择*首选项:打开用户设置(JSON)* 。

## 1.[自动重命名标签](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)—1050 万次下载

在撰写本文时，这个非常受欢迎的扩展已经有超过 1050 万次下载。我在每篇推荐扩展的博客文章中都看到了这个扩展。

然而，VS 代码通过内部设置提供了相同的功能。通过启用以下设置，您的标签将自动重命名，无需第三方扩展。

*注意:有人向我指出这个设置不能自动重命名 JSX/VUE 文件中的标签。对于这些文件，自动重命名标记扩展仍然是工具箱中一个有用的补充。*

## 2.[自动关闭标签](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag) — 8M 下载

与前一个扩展相同的作者的另一个非常受欢迎的扩展。随着时间的推移，这个扩展的功能也被添加到了 VS 代码中。

您可以使用以下设置在 JavaScript 或 TypeScript 中为 HTML 和 JSX 单独启用此设置:

## 3.[自动导入](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport)—250 万次下载

该扩展为 Typescript 和 TSX 中所有可用的导入自动查找、分析并提供代码操作和代码完成。

VS 代码中实际上有一堆设置帮助我们自动安排我们的导入。我们可以对 JavaScript/TypeScript 使用自动导入建议，在移动文件时更新导入，并在顶部使用绝对路径组织导入。

## 4.[设置同步](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) — 3.4M 下载

这个扩展对我来说是一个救命稻草，可以让我的 VS 代码设置跨机器同步。然而，VS Code 几乎在两年前就已经添加了这个特性。

关于如何设置的更多信息，请阅读[官方 VS 代码文档](https://code.visualstudio.com/docs/editor/settings-sync)。

## 5.[尾随空格](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)—110 万次下载

此扩展突出显示了训练空间，并允许您使用命令删除它们。

VS 代码有一个设置，如果启用，当你保存文件时会删除所有的尾随空格。这样你就不需要去想它们，也不需要高亮或者命令。您可以像这样启用设置:

## 6.[路径智能感知](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense&ssr=false#overview) — 8M 下载

这个扩展自动完成路径和文件名，有超过 800 万次下载。同一个开发者为 NPM 模块自动完成功能开发了一个类似的[扩展，下载量接近 500 万次。](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)

然而，像许多特性一样，VS 代码不久前添加了对这些特性的原生支持。默认情况下，这些功能是打开的，不需要启用任何设置。

## 7.[NPM](https://marketplace.visualstudio.com/items?itemName=eg2.vscode-npm-script)—560 万次下载

这个扩展允许您用命令运行 NPM 脚本。对于 Gulp、Make 等还有更多类似的扩展。它们可能是有用的，但是 VS 代码已经提供了一种处理这种情况的本地方式。VS 代码有一个特性叫做[任务自动检测](https://code.visualstudio.com/Docs/editor/tasks#_task-autodetection)。

任务可以自动检测或定制为通过命令面板或按下一个键绑定激活时自动运行。

[](/how-to-automatically-run-commands-in-visual-studio-code-300f2e4f144c) [## 如何在 Visual Studio 代码中自动运行命令

### 编辑描述

javascript.plainenglish.io](/how-to-automatically-run-commands-in-visual-studio-code-300f2e4f144c) 

## 8. [HTML 片段](https://marketplace.visualstudio.com/items?itemName=abusaidm.html-snippets)—840 万次下载

这个扩展允许你用速记快速放置 HTML 代码片段。相同的概念适用于以下两个扩展:

*   [CSS 片段](https://marketplace.visualstudio.com/items?itemName=joy-yu.css-snippets)
*   [HTML 样板文件](https://marketplace.visualstudio.com/items?itemName=sidthesloth.html5-boilerplate)

这些扩展都提供了速记版本，VS 代码本身已经支持这些版本。VS 代码内置了 [Emmet](https://docs.emmet.io/) 。Emmet 是一个神奇的工具，可以用容易记忆的快捷方式快速写出 HTML 和 CSS。

此外，Emmet 提供了现成的样板 HTML 模板，并允许您定义自己的定制代码片段。

## 9. [HTMLTagWrap](https://marketplace.visualstudio.com/items?itemName=bradgashler.htmltagwrap) — 415K 下载量

这个扩展和其他类似的扩展允许您选择一些 HTML 代码，并将其包装在一个标签中。这很有用，可以帮你在一天中节省几秒钟的时间。

VS 代码也通过 Emmet 命令提供了这一功能。只需用 CTRL/CMD + Shift + P 打开命令面板，寻找`Emmet: Wrap with abbreviation`。然后，您可以键入任何您想要的 emmet 缩写，这可以是单个标签，多个嵌套标签，带有类或 id 的标签。

## 10.[Lorem Ipsum](https://marketplace.visualstudio.com/items?itemName=Tyriar.lorem-ipsum)—47.3 万次下载

这个扩展允许您快速地将 Lorem Ipsum 文本块插入到您的标记中。

Emmet 的加入已经支持了这一点。你可以输入`lorem`，按 tab 键生成一个 30 字的段落。或者如果你需要多个块，你可以这样写来满足你的需要。

这将生成一个包含 3 个列表项的无序列表，每个列表项包含 30 个单词的段落。

## 11.[支架对着色机(1 & 2)](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer-2) — 5.2M 安装

括号对彩色和它的继任者一起有超过 1100 万安装。这与许多其他流行的括号着色扩展一起向 VSCode 团队展示了这是一个必须具备的特性。

这导致团队[在 VS 代码核心](https://code.visualstudio.com/blogs/2021/09/29/bracket-pair-colorization)中实现了括号对着色程序，据他们称，这使得速度提高了 10.000 倍。

通过启用以下设置，可以启用括号对颜色:

## 完整的设置列表

这里是上面提到的设置的完整列表。

## 结论

Visual Studio 代码有一个惊人的扩展市场，可以让您的生活更轻松。在安装其中一个之前，最好先看看它是否已经被本机支持。随着每月更新的发布，Visual Studio 代码的改进和特性将使更多的扩展变得不必要。每月花几分钟时间阅读发行说明将有助于您尽早发现这一点，并使您更熟练地使用您的编辑器。

感谢阅读。如果你对此有想法，一定要留下评论。

如果你喜欢我的内容并想支持我的努力，考虑通过[我的会员链接](https://medium.com/@WesleySmits/membership)成为一个媒体订阅者。这不会花费你任何额外的费用，但 Medium 会把部分收益给我，让我推荐你。

如果你愿意，你可以在 [LinkedIn](https://www.linkedin.com/in/wesley-robert-smits/) 或 [Twitter](https://twitter.com/iamwesleysmits) 上联系我！

[](https://medium.com/@WesleySmits/membership) [## 通过我的推荐链接加入 Medium-Wesley Smits

### 阅读韦斯利·斯密特(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

medium.com](https://medium.com/@WesleySmits/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***