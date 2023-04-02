# 如何在 Visual Studio 代码中自动运行命令

> 原文：<https://javascript.plainenglish.io/how-to-automatically-run-commands-in-visual-studio-code-300f2e4f144c?source=collection_archive---------5----------------------->

## 辅导的

## 使用 Visual Studio 代码任务使您的生活更加轻松

![](img/e628c666dd45dbe9c059656b5dc1dbbd.png)

有许多工具可用于自动化开发人员的任务，例如列出、构建、打包、测试和部署软件系统。这些例子有 NPM 脚本，吞咽，使，ESLint，网络包，和漂亮。

通常，这些命令从命令行运行，使开发人员能够快速访问需要采取的一系列步骤。有时，如果您可以直接从编辑器中运行这些命令，甚至可以自动确定它们应该何时运行，这可能会很有用。

这就是 Visual Studio 代码的任务功能发挥作用的地方。

## 用例

每天早上，当我跌跌撞撞地从床上爬起来时，我会拿起一杯咖啡，在 Slack 上给我的团队写一条早安消息，然后启动 VS 代码，在浏览器中打开我的本地开发 URL。

我似乎经常忘记的是启动 Webpack 来观察和构建我的资产。直到我做了一些 CSS 或 JS 的改变，我才注意到什么都没发生。(不要评价我，我一般早上 6 点就醒了😅)

在本文中，我想创建一个在打开 VS 代码时启动我的资产监视器的任务。这样我就可以免去一些自己制造的烦恼。

## 创建任务

您可以手动创建任务，也可以基于现有的自动检测脚本创建任务。例如，VS 代码已经识别了 NPM 脚本。

在这种情况下，我使用自动检测的 NPM 脚本作为模板。为此:

1.  打开命令选项板— CTRL / CMD + Shift + P
2.  选择配置任务选项—任务:配置任务
3.  选择要为其创建任务的 NPM 脚本

我为我的`start`脚本做了这个，它为我生成了下面的输出。

## 配置任务在启动时运行

现在，可以从命令面板运行该任务，但是它还不能在启动时运行。为此，我们应该向任务添加另一个规则。

每当你在 VS 代码中打开项目文件夹时，最后一行将运行这个命令，这样我们就有了一个工作的第一个任务。

## 创建自定义任务

有时自定义任务会很有用。让我们创建一个自定义命令来启动 Webpack watcher。

## 性能

让我们回顾一下我们刚刚使用的属性以及它们的含义。关于所有可能属性的完整列表，你可以阅读官方文档。

*   **标签** —用于 VS 代码界面中任务的标签。
*   **类型** —任务的类型，在我们的第一个任务中，这是 NPM，对于自定义任务，这可以是`shell`或`process`。
*   **命令** —您想要执行的实际命令。
*   **组** —允许你指定命令是属于`build`组还是`test`组。这使您可以更容易地从命令选项板运行命令。
*   **展示** —这定义了如何在用户界面中处理任务。您可以设置是否显示输出以及是否每次都在新的终端中显示输出。
*   **runOptions.runOn** —这定义任务应该手动运行还是在打开文件夹时运行。

## 复合任务

您还可以使用`dependsOn`属性创建由更小更简单的任务组成的任务。例如，如果您在客户端和服务器端都有一个构建脚本，并且希望在不同的终端上运行，那么您可以使用一个复合任务。

## 结论

Visual Studio 代码任务可能是工具箱中的一个有用工具。对我个人来说，最大的好处是当我打开一个项目时运行任务，这样我就不必在一天的第一杯咖啡时担心启动服务器和资产观察者。

感谢阅读。如果你对此有想法，一定要留下评论。

如果你喜欢我的内容，并想支持我的努力，考虑通过[我的会员链接](https://medium.com/@WesleySmits/membership)成为一个媒体订阅者。这不会花费你任何额外的费用，但 Medium 会把部分收益给我，让我推荐你。

如果你愿意，你可以在 [LinkedIn](https://www.linkedin.com/in/wesley-robert-smits/) 或 [Twitter](https://twitter.com/iamwesleysmits) 上联系我！

[](https://medium.com/@WesleySmits/membership) [## 通过我的推荐链接加入 Medium-Wesley Smits

### 阅读韦斯利·斯密特(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

medium.com](https://medium.com/@WesleySmits/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***