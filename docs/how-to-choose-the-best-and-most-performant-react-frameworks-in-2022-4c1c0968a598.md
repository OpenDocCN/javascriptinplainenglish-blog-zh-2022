# 如何在 2022 年选择最好和最具性能的 React 框架

> 原文：<https://javascript.plainenglish.io/how-to-choose-the-best-and-most-performant-react-frameworks-in-2022-4c1c0968a598?source=collection_archive---------7----------------------->

![](img/30ccbf6b5985e6b23f9d563cc94e9541.png)

Best React Starter

自 2013 年首次发布以来，React 越来越受欢迎。截至 2021 年，Statista 报告以 40.14%的采用率成为最受欢迎的 web 框架。随着它的流行，许多人试图在这个不固执己见的框架上发表意见。

因此，作为一名新的前端 web 开发人员，选择“最好的”React 框架/样板变得更加困难。在本文中，我将向您介绍高性能和生产就绪的库选择。

在设计现代 web 应用程序时，有许多重要的决策要做。主要是决定以下事项:

*   **React Bundler/trans piler/Boilerplates** 示例:Vite、Create React App、Next.js、Gatsby、Remix 等
*   **CSS 框架** 示例:Tailwindcss、样式组件、MUI、Antd、Bootstrap 等
*   **全局状态管理** 例子:重赛、反冲、Redux 工具包、MobX 等
*   **路由** 例子:React 路由器、React 导航、Wouter 等
*   **林挺/代码格式化程序** 示例:ESLint、Prettier 等
*   **IDE(带设置)** 示例:Visual Studio 代码、Atom、Webstorm、Notepad++等

如你所见，这个清单还在继续。这让所有的新开发者感到困惑，因为不可能花所有的时间去尝试这些库！因此，在本文中，我将讨论我对每个类别的首选以及设置它们的教程。我还将提供一个示例存储库。

为了实现高性能和快速的开发时间，我为所有想要构建响应性和可伸缩的 React web 应用程序的前端开发人员列出了以下库。

1.  [Vite |下一代前端工具](https://vitejs.dev/)
2.  快速建立现代网站，而不会让你的 HTML 离开 [DaisyUI](https://daisyui.com/)
3.  [Vite 插件页面|基于文件系统的⚡️Vite 路线生成器](https://github.com/hannoeru/vite-plugin-pages)
4.  [重赛| Redux 轻松搞定](https://rematchjs.org/)
5.  [Visual Studio 代码|代码编辑。重新定义。](https://code.visualstudio.com/)

在本节中，我将通过一步一步的教程来设置它们。如果您希望直接进行回购，请进入最后一部分。

## ***IDE 设置***

[下载](https://code.visualstudio.com/download)，安装 VSC。一旦你有了 VSC，安装以下扩展: [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) ， [Tailwind CSS Intellisense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

## ***新建一个 React 项目***

在本教程中，我们将创建一个 JavaScript 版本。但是，如果您愿意，可以随意创建一个类型脚本版本。

```
npm create vite@latest
? -> (y)
? -> type your project_name
? -> choose react
? -> choose react (react-ts for TypeScript)cd project_name
npm install
git init (if you want to initialise git)
npm run dev (if you want to start the project)
```

## ***安装 CSS 框架，实现有效、高效、准确的样式化***

```
npm install -D tailwindcss postcss autoprefixer daisyui
npx tailwindcss init -p
```

编辑以下文件:

## ***引入路由器并重新设计文件结构***

```
npm install -D vite-plugin-pages
npm install react-router react-router-dom
```

编辑以下文件:

创建以下文件夹并将 App.jsx 移动到 src/pages:

```
mkdir src/pages
mkdir src/components
mkdir src/redux 
mkdir src/hooks 
mkdir src/utils
mv src/App.jsx src/pages
```

编辑 App.jsx 导入路径:

## ***安装 ESLint 并允许林挺***

```
npm install eslint -D
npm init @eslint/config
? -> (y)
? -> To check syntax, find problems, and enforce code style
? -> JavaScript modules (import/export)
? -> React
? -> TypeScript No (Yes if using)
? -> Browser
? -> Answer Question
? -> JavaScript
? -> Space
? -> Single
? -> Unix
? -> No Semicolon
? -> yes to install
```

通过修改. eslintrc.cjs 向 ESLint 添加更多规则:

要在保存时启用自动林挺修复，请创建。vscode 文件夹，并将以下设置添加到。vscode/settings.json:

如果你一直追随到这里，恭喜你！您有一个自己安装的高性能 React web 应用程序。Vite 将通过`npm run dev`启动开发应用，比 CRA 或 Next.js 快得多

***对于使用 rematch.js 的最后一步，一定要自己尝试。您可以参考最后一节中的示例 GitHub 存储库。***

恭喜你走到了这一步！这是一个[存储库，供您开始使用](https://github.com/PrawiraGenestonlia/best-react-starter)。愿原力与你同在，帮助你开创下一个十亿美元的事业！⚡️⚡️⚡️

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****