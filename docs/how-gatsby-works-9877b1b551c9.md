# 盖茨比如何工作:指南

> 原文：<https://javascript.plainenglish.io/how-gatsby-works-9877b1b551c9?source=collection_archive---------15----------------------->

![](img/e4f92cbc412288c19b3d4b54af719398.png)

# 介绍

Gatsby 是一个静态站点生成器和 web 应用程序。这是一个基于 React 的开源框架。我们想知道盖茨比是如何工作的。在以下情况下使用非常合适:

*   我们正在建立投资组合网站
*   博客
*   公司主页。

下面是 Gatsby 中用于编译站点的两种模式。

1.  **开发:**在开发模式下，我们用`gatsby develop`命令运行
2.  **构建:**在构建模式下，我们用`gatsby build`运行

Gatsby 使开发人员能够从几乎任何内容或数据源快速获取和呈现内容。我们可以和盖茨比一起建网站；

*   单一堆栈
*   无论我们的内容生活在哪里。
*   这使我们能够利用 CMS 的丰富内容工作流。
*   因此，它不会被锁定在特定于 CMS 的开发生态系统中。
*   不记得代码冻结
*   Gatsby 将内容和数据变更从开发工作流中分离出来。

在本帖中，我们将解释 Gatsby 的生命周期是如何工作的，以及 Gatsby 特定文件的用途。

# 描述

[Gatsby 从我们提供的资源中提取数据，并为我们生成一个网站或应用程序。](https://www.technologiesinindustry4.com/)需要安装节点来运行引导程序和构建序列。Gatsby 利用 Webpack 构建并启动了一个开发服务器。盖茨比有三个阶段

1.  收集数据源
2.  建筑物
3.  部署

# 收集阶段

*   [在此阶段，it 将从来源收集数据。](https://www.technologiesinindustry4.com/)
*   来源是`Databases/XML files/CSV` / `Text files/JSON` / `WordPress`什么的。

# 建筑阶段

*   一旦收集了数据，我们就可以在 GraphQL 的帮助下从源代码中访问它。
*   我们可能不会改变现有的数据

# 部署阶段

*   我们可以建立开发后的应用程序。
*   我们可以在任何静态网站托管构建文件，如:
*   亚马逊 S3
*   网络生活
*   Github 页面
*   现在。上海和许多其他地方。

**盖茨比的生命周期**

以下三个序列组成了盖茨比的生命周期。

1.  [自举](https://www.technologiesinindustry4.com/)
2.  建设
3.  浏览器

# 主要特征

*   支持 Reactjs: Gatsby 支持 Reactjs，这将帮助我们构建可重用的组件，并使事情更容易控制。
*   **Webpack:** 这将有助于创建缩小和优化的捆绑包。
*   **SCSS 和 CSS-in-JS:** Gatsby 支持 SCSS，CSS-in-JavaScript 库，允许我们更好地管理样式。
*   **响应图像:**调整由设备组成的图像的大小。
*   **600 多个盖茨比插件:**有很多盖茨比插件可供`data sources/responsive-images/offline support/Mdx`和`analytics`等使用。
*   **支持 react 和 npm 包:**我们可以安装任何`npm`包，可以在 app 中使用。
*   **GraphQL:** Gatsby 从数据源收集数据，并通过 GraphQL 使其可用。数据源可以是任何东西`databases/json/XML/wordpress`或`text files`等。
*   **为用户提供更流畅的体验:**它将通过其功能为应用程序增加流畅度，旨在借鉴 PWA 的完整应用程序式体验。

# 盖茨比特定文件

**盖茨比-config.js**

*   放置所有站点配置的地方，例如插件、元数据和聚合填充。
*   这个文件是我们应用程序的蓝图。
*   gatsby-config.js 是我们运行 *$ gatsby develop* 或 *$ gatsby build* 时要读取和验证的初始文件

**盖茨比-node.js**

*   当我们开发或建立网站时，盖茨比会运行一个节点流程
*   它使用 Webpack 来启动一个带有热重载的开发服务器。
*   Gatsby 会在节点进程中加载插件。
*   它将分析缓存、引导网站并构建数据模式。
*   它将类似地创建页面，并处理不同的配置和数据管理。
*   在引导和构建序列过程中发生的一切都在 gatsby-node.js 中观察到。
*   这是动态创建由来自源插件的数据组成的页面的合适位置。

**盖茨比-ssr.js**

*   考虑服务器端呈现意味着我们会想到接受请求的服务器。
*   动态构建页面并将它们发送给客户端。
*   盖茨比不执行。尽管它在服务器端渲染上执行。
*   它在构建时创建所有页面。
*   Gatsby-ssr.js 使开发人员能够进入这个生命周期。
*   大多数用例属于将 CSS、HTML 或 Redux 状态信息注入到创建的输出中。

**盖茨比浏览器. js**

*   Gatsby 是一个静态站点，在第一次加载后加载一个动态应用程序。
*   这意味着我们在 web 应用程序中获得了静态站点的优势。
*   gatsby-browser.js 给出了处理 app 加载的便捷钩子。
*   它还提供路线更新、服务人员更新、滚动定位等等。
*   静态站点加载后发生的每一件事都可能在 gatsby-browser.js 中被钩住。

# 盖茨比入门

**先决条件**

*   Nodejs
*   [从 https://nodejs.org/en/download/](https://www.technologiesinindustry4.com/)下载

**安装 gatsby cli**

```
npm i -g gatsby-cli
```

*   在创建一个网站之前，我们应该先了解盖茨比。
*   开胃菜只是样板。
*   盖茨比的官方网站上有数百个样板或开胃菜。
*   [我们可以选择 Gatsby starter 作为；](https://www.technologiesinindustry4.com/)

**从 starter 创建新的 gatsby 站点**

```
gatsby new {name_of_your_site} {starter-repo-link}
```

*   当 `gatsby new`完成后，运行以下命令

```
cd {name_of_your_site}
gatsby develop
```

*   项目结构如下所示:

```
/
|-- /.cache
|-- /plugins
|-- /public
|-- /src
    |-- /pages
|-- /static
|-- gatsby-config.js
|-- gatsby-node.js
|-- gatsby-browser.js
```

*   最后，现在我们可以检查我们的网站在本地主机:8000。

更多详情请访问:[https://www.technologiesinindustry4.com](https://www.technologiesinindustry4.com)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*