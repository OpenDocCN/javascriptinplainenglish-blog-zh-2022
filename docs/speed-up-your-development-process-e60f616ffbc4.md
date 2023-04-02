# 介绍 Propulse:加速 React 开发过程的 NPM 软件包

> 原文：<https://javascript.plainenglish.io/speed-up-your-development-process-e60f616ffbc4?source=collection_archive---------13----------------------->

## 使用 Propulse 可以减少在项目设置和添加组件等耗时任务上花费的精力。

![](img/afa91f2ea0f2623ecdc0254465e8be75.png)

This is the header image

我是一个懒惰的人。最近有人说我非常懒惰，我同意这种说法。

我创建了一个 NPM 包，可以用来引导一个 React 项目。它维护了我在本文的[中描述的项目工作流。这是一种在项目设置和添加组件等耗时任务上花费更少精力的方式。](https://medium.com/@devriesrjj/how-to-structure-your-react-project-d33ea45772c1)

我给这个包起了一个史诗般的名字。它叫做: [Propulse](https://www.lexico.com/definition/propulse) 。

# 如何安装

安装很容易。你需要在系统上安装 [Node.js](https://nodejs.org/en/download/) ，这样你就可以自动使用 NPM 了。打开命令行工具，运行以下命令:

```
npm install -g propulse
```

这将安装 Propulse，使您可以在系统的任何地方使用它。有必要以管理员身份运行该命令。因此，如果你使用的是 Windows，请以管理员身份打开你的命令行。如果您使用的是 macOS，请运行以下命令:

```
sudo npm install -g propulse
```

# 启动项目

除了主动偷懒，我还蛮有想象力的。这意味着我经常开始一个新项目，并且不得不再次执行整个设置。Propulse 提供了引导整个 React 项目的选项。它节省了我很多时间。

导航到要在其中设置新项目的文件夹，并运行以下命令:

```
propulse create [projectName]
```

就是这样！现在会发生以下事情:

1.  正在使用 Create React App 设置 React 应用程序；
2.  将安装样式组件、Axios、React 路由器 Dom 和 env-cmd。
3.  将设置文件夹结构；
4.  将添加基本文件和内容。

# 添加新组件

我的反应大师教我“组件之道”。每个组件都有自己的文件夹，在这个文件夹中应该存放以下文件:视图、样式、索引和文本文件。保持整洁。

Propulse 允许我们使用 CLI 向项目添加组件。在项目的根目录中打开命令行，并运行以下命令:

```
propulse add
```

你现在会受到询问者的欢迎。您必须选择要添加的组件类型。之后，您必须为组件输入一个名称。确保遵循指定的命名约定。

# 最后的想法

你有它！Propulse 是我懒惰和挫败的产物。如果你遵循我在本文的[中讨论的项目结构，它应该会大大加快你的开发过程。](https://medium.com/@devriesrjj/how-to-structure-your-react-project-d33ea45772c1)

如果您有任何疑问、意见或其他任何问题，请告诉我。我很乐意讨论。

## 有用的东西

[](https://www.npmjs.com/package/propulse) [## 前脉冲

### Propulse 是一个 CLI 工具，既可以启动您的 React 项目，又可以加速您的开发体验。你将需要…

www.npmjs.com](https://www.npmjs.com/package/propulse) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*