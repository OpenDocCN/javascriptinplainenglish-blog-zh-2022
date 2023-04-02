# 设置开发环境的指南

> 原文：<https://javascript.plainenglish.io/a-guide-to-setting-up-the-development-environment-6313b9aa88?source=collection_archive---------10----------------------->

![](img/fad170c64a881203fe47239bdf8ed940.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 介绍

许多开发人员很难在他们的计算机上为自己建立一个良好的开发环境。这确实对学习有很大的影响，如果开发环境没有建立好，可能会阻碍学习的发展。在本文中，我将解释如何使用 **Github** 库来设置开发环境，以部署您的工作。

## **所需工具**

这是设置开发环境所需的工具列表，以下是对开发过程中所需工具的简要说明，以及每种工具如何简化工作:

1.一个网络浏览器
2。一个编辑
3。Git
4。一个 Github 账号
5。Node.js 和节点包管理器(npm)
6。浏览器同步

## **网络浏览器**

**什么是网络浏览器？**

用于访问万维网上的信息的软件应用程序被称为**网络浏览器**。当用户请求一些信息时，网络浏览器从网络服务器获取数据，然后在用户的屏幕上显示网页。

每个 windows 系统都有一个默认的网络浏览器，那就是微软 edge。微软 Edge 是一个很好的网络浏览器，由微软制造，它支持最新的 HTML 版本，HTML5。你将在你的开发中使用网络浏览器，这是非常必要的。因为你要用它来下载、显示和测试你的网站和许多其他东西。

[点击这里](https://www.google.com/chrome/)获取 chrome 并安装。

## **一名编辑**

编辑器是你为你的网站写代码的工作空间。Windows 系统自带的默认编辑器是**记事本**。互联网上有许多免费的编辑器可供下载，例如 Visual Studio Code(也称为 VSCode)、Sublime、Atom 等等。你可以下载这些编辑器，测试它们来选择你最喜欢的。不过我更喜欢 VSCode。

[点击此处](https://code.visualstudio.com/Download)下载 VSCode，并确保下载后安装。

## Git

Git 是一个免费的开源分布式版本控制系统，旨在快速高效地处理从小到大的项目。

Git 易于学习，占用空间小，性能快如闪电。它比 Subversion、CVS、Perforce 和 ClearCase 等配置管理工具具有更便宜的本地分支、方便的中转区和多工作流等特性。

我将解释您开发所需的 git 命令，但是您可以在这里阅读更多关于 git [的内容。](https://git-scm.com/)

要下载 **git** ，请访问 [git 网站](https://git-scm.com/downloads)点击 downloads 并选择与你的电脑相匹配的选项。然后，你必须把它安装在你的电脑上。

## **一个 Github 账号**

**Github 公司**。是一家使用 Git 进行软件开发和版本控制的互联网托管提供商。它提供了 Git 的分布式版本控制和源代码管理功能，以及它自己的特性。它为每个项目提供了访问控制和几个协作功能，如错误跟踪、功能请求、任务管理、持续集成和 Wikis。总部位于加州，自 2018 年以来一直是微软的子公司。

我们将使用 Github 来部署我们的工作。

## **Nodejs 和节点包管理器(NPM)**

Node.js 是一个开源、跨平台的后端 JavaScript 运行时环境，运行在 V8 引擎上，在 web 浏览器之外执行 JavaScript 代码。Node.js 允许开发人员使用 JavaScript 编写命令行工具和服务器端脚本，即在页面被发送到用户的 web 浏览器之前，在服务器端运行脚本来生成动态网页内容。因此，Node.js 代表了一种“无处不在的 JavaScript”范例，[6]围绕一种编程语言统一了 web 应用程序开发，而不是针对服务器端和客户端脚本的不同语言。

我们需要 **Node.js** 来管理我们的环境。

下面是你电脑上下载 nodejs 的链接: [Node.js 下载链接](https://nodejs.org/en/download/)。选择与您的计算机匹配的选项并下载。

## **浏览器同步**

谷歌浏览器同步是作为谷歌免费软件发布的 Mozilla Firefox 扩展。它于 2006 年 6 月 8 日在谷歌实验室首次亮相，2008 年 6 月停止使用。它允许 Mozilla Firefox 2 . x 版本的用户通过互联网在多台计算机上同步他们的网络浏览器设置。

我们需要它来不时地检查我们代码中的变化，而不必刷新我们的浏览器。如何安装浏览器同步的指南将包含在接下来的分步指南中。

接下来是设置我们的**开发环境**的一系列指南

## 注意:

## 设置我们的开发环境

说明:确保你已经下载了安装所需的所有文件

**步骤 1** -
导航到您的窗口，搜索`cmd`，这是命令提示符，打开它，让我们开始吧。

**第 2 步**
首先检查所需文件是否已经在您的电脑上。

-要检查 git，在命令行中键入`git-version`,它将显示您计算机上的 git 版本。

-键入`node-version`来检查节点，最后，

-键入`npm-version`以检查节点程序包管理器。

确认所有所需文件后，您可以继续下一步。

**第三步**
下载**浏览器同步**。为此，请访问浏览器同步网站，将页面上的命令行复制到您的命令提示符 *cmd* 中进行下载。

**第 4 步**
导航到您的浏览器并登录您的 Github 帐户。登录后，单击右上角的+号创建一个存储库。

**第 5 步** -
为您的存储库命名，向下滚动一点点，然后单击**添加自述文件**向存储库添加一个自述文件。

**第 6 步**
导航至**设置**然后导航至**页面。**在 pages 屏幕上，导航至 sources 并点击它，然后将分支更改为 **main。**点击**改变主题**，它会带你到 Github 主题页面。选择一个主题并提交。

**第 7 步**
导航到您的存储库的主页并复制链接。

**第八步**
接下来就是去你的 cmd，键入`**git-clone**` 然后粘贴到链接里，添加`.git`到里面克隆出来。

**第 9 步**
`git-status` —用于检查您的存储库的状态。

`mkdir` —用于创建新文件。

`dir` —用于检查当前存储库目录中的文件。

`git-add .` —用于添加新文件。

`git-commit -m "msg"` —用于通过消息 **msg 提交变更。**

`git-push` —用于推送变更，完成您 Github 账户上的变更。

**第 10 步**
接下来就是转到你的 cmd，键入`**git-clone**` 然后粘贴到链接里，添加`.git`到里面就可以克隆了。

现在只需输入`code .`打开你的代码编辑器，开始编码

**第 12 步**
现在你已经设置好了。查看步骤 9，了解在线发布代码所需的命令。

要访问指向您站点的链接，请转到存储库的设置，导航到页面并复制链接。

感谢阅读。

请随时在以下社交媒体上联系我: [Twitter、](https://twitter.com/devtoheeb) [脸书](https://www.facebook.com/akande.olalekan.1238)、 [Instagram](https://www.instagram.com/muh_toyyib_0/) 或 [WhatsApp。](https://wa.me/message/BUW6NXAJ2A3HA1)

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*