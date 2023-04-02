# Gitlab CI 上带有 MegaLinter 的 Node.js 编码标准工具

> 原文：<https://javascript.plainenglish.io/node-js-coding-standard-tools-with-megalinter-on-gitlab-ci-a43b55915811?source=collection_archive---------10----------------------->

![](img/fe1be4cafc4b4d0ef986ee5e0703a980.png)

Photo by [Desola Lanre-Ologun](https://unsplash.com/@disruptxn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我们的应用程序的整个生命周期和不断变化中，保持它的可读性、稳定性、高性能和可维护性是一个持续的斗争，同时每天都在发展以提供更多的选项和功能。

最重要的是，开发应用程序的团队也在发展。团队成员将上下文从应用程序的一部分切换到另一部分，他们离开团队，新的团队成员加入。

为了解决这些挑战，我们利用编码标准工具来帮助我们遵守我们为应用程序定义的标准和规则。

Node.js 应用程序的一些最重要的工具是 [EsLint](https://eslint.org/) 、 [CSpell](https://cspell.org/) 、 [Dockerfilelint](https://hadolint.github.io/hadolint/) 、 [JSCpd](https://github.com/kucherenko/jscpd) 和[pretty](https://prettier.io/)。所有这些工具也可以与 MegaLinter 结合在一起，这样我们就可以一次性自动检查所有这些规则。

所有这些工具也可以在我们的 IDE 中通过使用不同的插件/扩展来配置。下面是它们各自对我喜欢的 Node.js IDE 的扩展: [EsLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) ， [CSpell](https://marketplace.visualstudio.com/items?itemName=RemiMarche.cspell-tech) ，[beautiful](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)，[Hadolint](https://marketplace.visualstudio.com/items?itemName=exiasr.hadolint)——作为 docker 文件 linter。

不幸的是，JSCpd 在市场上不再可用，但是如果你想用它来创建扩展，可以在 GitHub 上找到源代码。我个人是不用这个的。

事不宜迟，让我们分别深入每个工具，看看一个配置示例，以及它能为我们做些什么来帮助改进代码库。

# 埃斯林特

众所周知，这个工具通过在违反规则时发出警告或错误来帮助我们确保我们的代码遵循 ECMAScript 和 JavaScript 代码模式。我经常使用的这个工具的配置如下。正如您从配置中看到的，它用于验证 TypeScript 代码。

# 切斯佩尔

这个工具用于检查我们的代码拼写是否正确。它支持各种编程语言，其中包括 TypeScript 和 JavaScript。我对这个工具的配置如下所示。如你所见，我们可以忽略某些路径或单词，这些路径或单词是以某种方式书写的，并且不是语法正确的英语单词。

# Dockerfilelint

该工具将 Dockerfile 文件解析成 AST(抽象语法树),并在其上执行规则。它依靠 [ShellCheck](https://github.com/koalaman/shellcheck) 将 Bash 代码嵌入到`RUN`指令中。下面是我用来检查 Dockerfile 语法的配置。

# JSCpd

作为开发人员，我们都知道大多数时候使用复制粘贴和过度使用它的斗争。这个工具确保我们尽可能避免使用复制粘贴。它支持超过 150 种不同的编程语言。这是我用于这个工具的配置。

# 较美丽

正如我们许多人所知，这个工具是一个代码格式化程序。与其他工具一样，这个工具也支持多种编程语言，但是对于我正在使用的 TypeScript 和 JavaScript，我的配置非常简单，它只检查三个规则。

# 米加林特

这个工具在一个地方将所有以前的工具结合在一起，这样我们可以一次执行它们，而不用担心我们忘记了其中的一个。它的主要目的是在 CI/CD 中执行，但也可以在本地使用。它支持多种编程语言(50 种左右)、多种不同的代码格式(20 种左右)、多种编码标准工具(20 种左右)。如果我们对它进行配置，它还会自动修复所有报告的问题。在这种情况下，我仅将它用于依赖 JavaScript 和 TypeScript 的 Node.js 应用程序，我对该工具的配置如下:

最后但同样重要的是，git lab CI configuration for mega linter 确保我们在应用程序上进行的每一次代码更改都遵循上述工具的所有规则。

希望分享这些工具和我正在使用的设置对我有所帮助:-)

![](img/1237de54086be46b6cf8a8c7d2bbde47.png)

Photo by [Jay-Pee Peña 🇵🇭](https://unsplash.com/@jpineapplepen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***