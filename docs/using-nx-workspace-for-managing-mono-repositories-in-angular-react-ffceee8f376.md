# 如何在 Angular/React 中使用 Nx Workspace 管理 Mono 存储库

> 原文：<https://javascript.plainenglish.io/using-nx-workspace-for-managing-mono-repositories-in-angular-react-ffceee8f376?source=collection_archive---------9----------------------->

![](img/8f21aece817df40a89afdde5e7f43b53.png)

最近有很多关于 **mono 库**的讨论。我想我应该阐明这个概念，以及如何使用 **Nx workspace** 在任何前端和后端框架中利用它们。

那么，什么是真正的**单声道储存库**？

> Mono Repository 是一种软件开发技术，其中软件开发人员在共享存储库中编写代码，这些代码可以跨多个应用程序使用，而不必为每个应用程序编写代码。

**举例:**

假设我们有一个大型企业级应用程序，该应用程序被分成两个不同的子应用程序。一个是名为**客户应用**的应用，另一个是**仪表盘应用**。这两个应用程序有相同的页眉和页脚，使用套接字、地图等。在这种情况下，我们不是为这两个应用程序编写单独的页眉和页脚，而是将它们编写在一个共享的存储库中，然后在这两个应用程序中使用它们。

还有，什么是 **Nx 工作空间**？

> Nx 是 Angular、React 等应用的工作空间。，这允许我们实现单一存储库的概念。

![](img/c42ed5c47689472f44b15522613e7009.png)

让我们看看实际的代码。我将使用 **Angular** 向您展示一个示例，但是对于 **React、Vue、**等，实现保持不变。，以及任何其他后端框架。

通过运行以下命令，在您喜欢的目录中创建一个 Nx 工作区:

![](img/be82c36ae98425044d2f23d2f46121e3.png)

这将显示多个选项:

![](img/b410421afbcb4182e38fa53e96d8b985.png)

从上面，我将选择角度。

![](img/d284a8d26c253f9956f0ed21c58d7828.png)

命名您的应用程序。我将使用名称**客户应用**。

在 Visual Studio 代码中打开目录。

![](img/4e264b55cc9e18a66c0be4cb375800a5.png)

这是应用程序的结构。这里， **apps** 目录包含单个或多个应用程序，而 **libs** 目录是一个共享存储库。

现在，让我们创建另一个名为**仪表板应用程序**的应用程序。运行以下命令:

![](img/3546342785a2350608d53c2255919820.png)

这将在同一目录中创建第二个应用程序。这是新的结构。

![](img/a7e208c34966cb66a6346d3d16d8ae29.png)

现在，在 **libs** 目录中创建您想要在两个应用程序中使用的任何内容。出于演示的目的，我将使用 web 上的一些卡代码创建一个简单的卡组件。为此，让我们首先在 libs 目录中创建一个名为 **UI** 的库。运行以下命令。

![](img/253a7903fbebba2db852a163926af12a.png)

你可以在下面看到我们的图书馆已经创建。该结构看起来像这样:

![](img/625fb1a30a3a91ad01219f84ff5f8620.png)

现在，通过运行以下命令在库中创建一个组件:

![](img/3facf5c9aba33945a4b0a3c2f2c3c1c6.png)

该结构看起来像这样:

![](img/c99af674ad9df72a0222f7ddd95684a2.png)

在演示卡中添加一些 HTML 和 CSS 后，将组件添加到 **ui.module** 文件中的 **exports** 数组中。

![](img/1bb6ff5ee0d60ae7f955835a1d6fa557.png)

在**客户**和**仪表盘应用**的 app.module 中导入整个 **ui** **模块**，如下图所示。

![](img/7867361ead6869e6dfd76ec6353073ae.png)

利用**客户**和**仪表板 app** 的**app.component.html**文件中的演示卡组件选择器。

![](img/234fc270732245443c7f3c0c4dec1106.png)

通过在单独的终端中使用这两个命令来运行这两个单独的应用程序。

![](img/4844f608c875923944fa2352a8250ddb.png)![](img/59d42b702fc5647414dc44147aad52e9.png)

我们得到了下面运行的两个应用程序的输出。

![](img/5feff5e80eedc6690ddd49b84b10811d.png)

**结论:** 上面的例子展示了我们可以通过创建一个 mono 存储库在两个不同的应用程序中使用相同的代码。Nx workspace 允许我们编写可重用的代码，帮助我们增强应用程序的性能并显著减小其整体大小，从而使我们的生活变得更加轻松。

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*