# 16 个命令可在几秒钟内为每个用例设置 React 应用程序⚡🚀

> 原文：<https://javascript.plainenglish.io/16-commands-to-set-up-react-apps-for-every-use-case-in-seconds-aba7d0017700?source=collection_archive---------15----------------------->

![](img/1629b9a2cffc4a1df14292be1114f9d0.png)

今天，速度是击败竞争对手的主要标准之一。随着技术变得越来越复杂，我们花费越来越多的时间来设置和配置一切。

在这篇文章中，我精心挑选了 16 个命令来在几秒钟内设置 React 应用程序。我试图涵盖您在开发人员工作流程中可能面临的不同用例的各种工具。

本文中包含的大多数工具都是开源的。我将为您提供直接访问链接、工具描述以及从终端运行它们的命令。

## [创建-反应-应用](https://github.com/facebook/create-react-app)

一种官方支持的创建单页 [React](https://reactjs.org/) 应用程序的方式。它提供了一个没有配置的现代构建设置。

```
npx create-creact-app project-name
cd project-name
npm start

# starts on port 3000
```

## [纳米反应 app](https://github.com/nano-react-app/nano-react-app)

对 [Create-React-App](https://create-react-app.dev/) 的真正最小替代。一个完整的[反应](https://reactjs.org/)项目只有 6 个文件。使用零配置的 [ViteJS](https://vitejs.dev/) 代替 [Webpack](https://webpack.js.org/) 。没有弹射，没有林挺，没有服务人员。

```
npx nano-react-app project-name
cd project-name
npm install
npm start

# starts on port 3000
```

## [反应启动器套件](https://github.com/kriasoft/react-starter-kit)

用 [React](https://reactjs.org/) 、 [Relay](https://relay.dev/) 和 [GraphQL](https://graphql.org/) 构建 web 应用的 web 最流行的前端模板。基于 [JAM 栈](https://jamstack.org/)架构。

```
git clone -o seed -b main --single-branch https://github.com/kriasoft/react-starter-kit.git project-name
cd project-name
npm install
npm start

# starts on port 3000
```

## [反应-样板文件](https://github.com/react-boilerplate/react-boilerplate)

一个高度可扩展的、离线优先的基础，具有最佳的开发人员体验，并关注性能和最佳实践。

```
git clone --depth=1 https://github.com/react-boilerplate/react-boilerplate.git project-name
cd project-name
npm run setup
npm start

# starts on port 3000
```

## [中微子](https://github.com/neutrinojs/neutrino)

它使用 [Webpack](https://webpack.js.org/) 构建 web 和 [Node.js](https://nodejs.org/en/) 项目，提供完整的构建预置，可以在目标和项目之间共享。

```
npx @neutrinojs/create-project project-name
# pick react from the wizard
cd project-name
npm start

# starts on port 5000
```

## [狂欢](https://github.com/jaredpalmer/razzle)

一个工具，它抽象了构建 SPA 和 SSR 应用程序所需的所有复杂配置。它将应用程序关于框架、路由和数据获取的架构决策留给了您。

```
npx create-razzle-app project-name
cd project-name
npm start

# starts on port 3000
```

## [创建-反应-库](https://github.com/transitive-bullshit/create-react-library)

使用 [Rollup](https://rollupjs.org/guide/en/) 创建可重用的现代 [React](https://reactjs.org/) 库的 CLI。

```
npx create-react-library 
# enter project-name as a title in wizard
cd project-name
npm start

# runs `rollup` with the watch flag to recompile your source on changes, no port used
```

在单独的终端运行另一个服务器进行预览的例子:

```
cd project-name/example
npm start

# starts on port 3000
```

## [tsdx](https://github.com/jaredpalmer/tsdx)

一个零配置 CLI，帮助您轻松开发、测试和发布 modern [TypeScript](https://www.typescriptlang.org/) 包——这样您就可以专注于您出色的新库，而不必在配置上再浪费一个下午。

```
npx tsdx create project-name 
# choose react as a template in the wizard
cd project-name
npm start

# runs in watch mode to recompile your source on changes, no port used
```

## [react-pwa](https://github.com/Atyantik/react-pwa)

一个用于渐进式 web 应用程序(PWA)的可升级样板，具有服务器端呈现功能，构建时考虑了 SEO，实现了最高的页面速度和优化的用户体验。

```
git clone https://github.com/Atyantik/react-pwa.git project-name
cd project-name
npm install
npm start

# starts on port 9090
```

## [rekit](https://github.com/rekit/rekit)

使用 [React](https://reactjs.org/) 、 [Redux](https://redux.js.org/) 和 [React-router](https://reactrouter.com/) 构建可伸缩 web 应用的工具包。通过使用面向功能的架构，每个文件模式一个动作，它被设计成可伸缩、可测试和可维护的。

```
npm install -g rekit  # install rekit cli
npm install -g rekit-studio  # install rekit studio

rekit create project-name
cd project-name
npm install
rekit-studio -p 3000

# starts on port 3000
```

## [反应-燃烧基-启动器](https://github.com/kriasoft/react-firebase-starter)

用 [React](https://reactjs.org/) 、 [GraphQL](https://graphql.org/) 和 [Relay](https://relay.dev/) 创建 web 应用的样板项目。

```
git clone https://github.com/kriasoft/react-firebase-starter.git project-name
cd project-name
npm setup
npm start

# starts on port 3000
```

## [电子反应样板](https://github.com/electron-react-boilerplate/electron-react-boilerplate)

可扩展跨平台应用的基础。采用[电子](https://electron.atom.io/)、[反应](https://facebook.github.io/react/)、[反应路由器](https://github.com/reactjs/react-router)、[网络包](https://webpack.js.org/)和[反应快速刷新](https://www.npmjs.com/package/react-refresh)。

```
git clone --depth 1 --branch main https://github.com/electron-react-boilerplate/electron-react-boilerplate.git project-name
cd project-name
npm install
npm start

# starts on port 1212
```

## [创建-反应-原生-应用](https://github.com/expo/create-react-native-app)

专注于以最快的方式引导运行在 iOS、Android 和 web 上的 [React 原生](https://reactnative.dev/)应用，而无需担心开发和发布应用所需的原生平台或捆绑器。

```
npx create-react-native-app
# set the name to project-name in the wizard
cd project-name
npm run web

# starts on port 19006
```

## [创建下一个应用](https://nextjs.org/docs/api-reference/create-next-app)

最简单的入门方法是从 [Next.js](https://nextjs.org/) 开始。你可以使用默认的 Next.js 模板，或者使用官方的 Next.js [示例](https://github.com/vercel/next.js/tree/canary/examples)来创建一个新的应用。

```
npx create-next-app project-name
cd project-name
npm run dev

# starts on port 3000
```

## [gatsby.js](https://github.com/gatsbyjs/gatsby)

基于 [React](https://reactjs.org/) 的免费开源框架，帮助开发者构建超快的网站和应用。它将动态呈现站点的控制和可伸缩性与静态站点生成的速度结合起来。

```
npm install -g gatsby-cli # install gatsby cli

gatsby new
# set the name to project-name in the wizard
cd project-name
gatsby develop

# starts on port 8000
```

## [闪电战](https://github.com/blitz-js/blitz)

受 [Ruby on Rails](https://rubyonrails.org/) 的启发，一个包含电池的框架构建在 [Next.js](https://nextjs.org/) 之上，具有零 API 数据层抽象，消除了对 REST/GraphQL 的需求。

```
npm install -g blitz --legacy-peer-deps # install blitz cli

blitz new project-name
cd project-name
blitz dev

# starts on port 3000
```

希望您会发现这些说明中有一些是有用的，这样您就可以在设置工作空间上节省大量时间，并完全专注于实际的编码。

写作一直是我的激情所在，帮助和激励他人给我带来了快乐。如果您有任何问题，请随时联系我们！

在 [Twitter](https://twitter.com/madzadev) 、 [LinkedIn](https://www.linkedin.com/in/madzadev/) 和 [GitHub](https://github.com/madzadev) 上给我接通！

访问我的[博客](https://madza.dev/blog)获取更多类似的文章。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***