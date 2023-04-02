# 每个开发人员都应该使用的 6 个软件开发工具

> 原文：<https://javascript.plainenglish.io/6-software-development-tools-every-developer-should-use-35f7ac771bad?source=collection_archive---------2----------------------->

## 不管你在做哪个项目，或者和多少人一起工作，你都应该使用这六个开发工具。

![](img/235ddcbdd3e07926d956fcd61a74745e.png)

Thumbnail by The Soggy Waffle

蹩脚代码的日子已经一去不复返了。当计算机第一次出现的时候，在接下来的几十年里，如果你的代码工作正常，一切都很好。现在项目规模很快，功能代码不一定好。IDE 是最流行的开发工具，但是仅此一项已经不能帮助我们了。现在，我们需要插件、外部软件和扩展来完成工作并提高效率。

这里有六种你需要使用的开发工具，以及每种工具的基本原理。此外，我还包括了一些替代方案。

# 饭桶

[](https://git-scm.com) [## 饭桶

### Git 易于学习，占用空间小，性能快如闪电。它远胜于 Subversion 等配置管理工具…

git-scm.com](https://git-scm.com) [](https://github.com) [## GitHub:世界构建软件的地方

### GitHub 是 8300 多万开发者共同塑造软件未来的地方。为开源做贡献…

github.com](https://github.com) 

这是一个给定的，但它有一个很好的理由在这个列表中排名第一。如果你还没有使用 Git，你就失败了。Git 是一个跟踪代码变化的版本控制系统。它面向所有人，从个人开发者到大型组织。

## Git 的优势

*   **跟踪您的代码变更**——如果您的当前代码和先前版本之间出现问题，您可以通过查看您的代码变更历史来快速定位错误。
*   **简单的恢复和回滚** —如果你对你的软件做了大量的修改，并且在这个过程中有很多东西损坏了，你可以放弃你所有的修改。如果需要备份几个版本，可以将整个 git 存储库回滚到前一个版本。
*   **远程存储库** —远程存储库将为您托管您的代码。如果您正在一台新的机器上工作，您可以很容易地克隆这个库并重新开始工作。
*   GitHub 是一个远程仓库，允许你向全世界展示你的作品。如果您不喜欢这样，您可以使用私有存储库。您还可以访问 CI/CD 功能、Wikis 等等。

## Git 的替代品

*   微软 TFS 公司
*   Azure DevOps 服务器
*   AWS 代码提交
*   破坏

# 较美丽

[](https://prettier.io) [## 更漂亮的固执己见的代码格式化程序

### 固执己见的代码格式化程序

固执己见的代码格式](https://prettier.io) 

Prettier 是一个代码格式化程序，带有大多数 ide 的扩展。开箱即用，它支持 web 开发所需的语言。此外，您可以安装其他语言的插件。您可以通过修改编辑器设置中的配置来使 Prettier 符合您的编码风格，或者通过在项目的根目录下创建一个`.prettierrc`文件来使设置特定于项目；否则，你可以坚持漂亮的默认设置。每次你保存一个文件，漂亮会自动格式化你的代码并保存它。

## 更漂亮的优点

*   **自动代码格式化** —当你保存任何源文件时，Prettier 会自动格式化。
*   **标准代码风格** —组织可以为每个项目配置一个更漂亮的配置，以保持标准化和结构化的代码风格。此外，可以定义特定于项目的代码样式。
*   **更小的 Git 提交** —因为同一组织中的每个人都使用相同的漂亮配置，所以所有代码在每次提交时都以相同的方式格式化。Git 提交将只包括基本的代码更改，而不仅仅是格式或代码风格的更改。
*   **防止坏的/难看的代码**—prettle 是一个“固执己见”的代码格式化程序。它将强制您的代码风格与最佳编码实践相匹配。*但是，如果你想覆盖它们的默认设置，你可以。*

## 更漂亮的替代品

*   编辑器配置
*   黑色(仅适用于 Python)

# 埃斯林特

[](https://eslint.org) [## 查找并修复 JavaScript 代码中的问题

### 一个可插入和可配置的 linter 工具，用于识别和报告 JavaScript 中的模式。维护您的代码…

eslint.org](https://eslint.org) 

林挺软件是 JavaScript 代码的同义词。有许多 JavaScript linter:JSHint、JSLint、ESLint、TSLint 等等。这些有什么问题？它们都不像 ESLint 那样可配置或先进。TypeScript 过去使用 TSLint 来处理林挺的 TypeScript 代码，但现在他们使用 ESLint 和一个 TypeScript 插件。

如果您还不知道的话，ESLint 会捕捉代码中的代码风格问题和潜在的 bug。通过一个简单的标志(`--fix`)，ESLint 将自动修复它所能修复的任何错误或代码风格问题——尽管它不能完全取代 Prettier。有些 bug、错误或警告必须手动修复，但至少 ESLint 会帮你找到它们。

## ESLint 的优势

*   发现潜在的错误和漏洞
*   查找错误和警告
*   实施良好的代码风格
*   自动解决问题
*   风格报告

## 可供选择的事物

*   JSLint
*   JSHint
*   TSLint

# 终点站

终端是另一个给定的。一些人喜欢使用`vim`在他们的终端中编写代码，而另一些人则用它来执行命令。其他人更喜欢使用 GUI。但是如果您想克隆一个 GitHub 存储库，安装一个`npm`包，并快速移动/复制匹配 blob 模式的文件呢？当然，你可以对每一个都使用 GUI，但是这是最有效的方法吗？

安装一个`npm`包应该只需要 5 秒钟就可以在命令行中写出来，但是在使用 GUI 时(包括启动 GUI)需要 45 秒钟。克隆一个 GitHub 库通常需要大约 5 秒来编写命令，另外需要 10 秒来下载源代码；总共 15 秒。启动 GitHub 桌面客户端需要 15 秒。终端是你完成大多数任务的最好朋友。

这并不意味着终端永远是你最好的朋友。有时，GUI 会使开发变得不那么复杂。有时命令需要许多标志或参数，而 GUI 简化了这个过程。无论您的用例是什么，如果您看到自己使用 GUI 足够经常地重复一个简单的任务，尝试学习如何在终端中完成它；你可能会发现它更容易接近。

# DevUtils

[](https://devutils.app) [## DevUtils.app -面向开发人员的多功能工具箱

### 强大的开发工具，帮助您完成日常任务。原生 macOS 应用，离线工作，尊重你的数据。

devutils.app](https://devutils.app) 

DevUtils 是一个 Mac 应用程序(我敢肯定 Windows/Linux 有一个替代品),拥有开发人员需要的一切。它是开发人员实用工具的瑞士军刀，有如此多的特性，我无法一一介绍。我经常发现自己将 HTML 代码复制到我的 React TSX 项目中。所以，每天我都使用 DevUtils 将我的 HTML 转换成 JSX 友好的(比如将`class`属性改为`className`)。

## 我最喜欢的功能

*   JSON 格式化/验证
*   JSON Web 令牌(JWT)调试器
*   正则表达式测试器
*   URL 编码器和解码器
*   URL 解析器
*   反斜杠转义和不转义
*   UUID 发生器和解码器
*   文本差异检查器
*   JSON 到 YAML(反之亦然)
*   JSON 到 CSV(反之亦然)
*   基数转换器
*   许多语言的美化器和缩小器
*   Lorem Ipsum 生成器
*   QR 码阅读器和生成器
*   字符串检查器
*   哈希生成器
*   HTML 到 JSX
*   降价预览
*   SQL 格式化程序
*   更多的

# VS 代码

[](https://code.visualstudio.com) [## Visual Studio 代码-代码编辑。重新定义的

### Visual Studio Code 是一个重新定义和优化的代码编辑器，用于构建和调试现代 web 和云…

code.visualstudio.com](https://code.visualstudio.com) 

拥有成千上万我们永远不会用到的功能的笨重 ide 的时代已经一去不复返了。VSCode 是我们唯一需要的 IDE。就其本身而言，它只是一个简单的代码编辑器。但是当你安装了扩展，它就变成了一个发电站和一个成熟的 IDE。你可以用任何语言为任何项目编写代码，VS 代码将提供语法高亮和插件支持。此外，在代码完成方面，IntelliSense 比其他 ide 精确得多。

## 优势

*   每个 IDE 中最大的扩展库
*   非常可定制
*   智能感知
*   使用方便
*   快速响应
*   简单的键盘快捷键和命令面板
*   多重选择和多重编辑
*   直观的用户界面
*   支持每种语言

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*