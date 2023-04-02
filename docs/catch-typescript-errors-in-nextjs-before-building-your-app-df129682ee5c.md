# 在构建应用程序之前，捕获 Next.js 中的 TypeScript 错误

> 原文：<https://javascript.plainenglish.io/catch-typescript-errors-in-nextjs-before-building-your-app-df129682ee5c?source=collection_archive---------2----------------------->

## 自动执行任务以捕捉 Next.js 中的类型错误

![](img/a17aebc4199182d85e481b240bc1e556.png)

最近，我们在西北图书馆的开发团队已经在我们的 UI 应用程序中过渡到类型脚本。当开发环境看起来运行良好时，我们已经遇到了两次 CI 构建失败的“陷阱”。这是一个简单的解决方案，但可能会节省你一点时间和挠头。

# 问题

应用程序代码库在本地开发模式下成功运行，但是当被推送到应用程序的 CI ( [持续集成](https://en.wikipedia.org/wiki/Continuous_integration))管道时，在暂存基础上构建会失败。

嗯。我们像一个负责任的开发人员一样运行 Next.js 的预连线`next lint`脚本，一切都没问题。我们尝试 Next.js 的`next build`脚本，它就在那里；构建失败。

# **手动解决方案**

一个解决方案是记得在每次`git`提交之前手动运行`next build`，因为`next build`似乎在某种程度上捕捉到了打字错误。(至少我自己)记得每次手动运行这个的机会？不太好。

# 或者…自动化解决方案

如何在 Next.js 中自动执行这项任务，在为 pull 请求推送代码之前捕捉类型错误，甚至不去想它？

一种选择是设置*一个* [*预提交钩子*](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks#:~:text=The%20pre%2Dcommit%20hook%20is,to%20inspect%20in%20the%20code.) *。*

在实际提交发生之前，预提交挂钩将在`git commit`运行。

一个常见的用例是运行测试(单元或集成)，作为提交前的钩子动作，以自动化测试覆盖率的保证。然而，我们想要的是在 git 提交发生之前将*类型检查*添加到代码中。

如前所述，默认的 Next.js 配置是预先绑定了一个`next lint`命令的。该命令将根据您的 [ESLint 配置](https://eslint.org/)捕获 JavaScript 错误，但是 ESLint 配置不会自动识别 TypeScript，即使在使用 TypeScript 引导您的 Next.js 应用程序时也是如此。

# 代码

让我们添加一些代码来帮助解决这个问题。这是假设您的 Next.js 应用程序配置为使用 TypeScript。如果是这样，您将可以访问 TypeScript [命令行编译器工具](https://www.typescriptlang.org/docs/handbook/compiler-options.html)、`tsc`。

将下面一行添加到您的`package.json`文件的`scripts`块中:

```
”ts-lint”: “tsc — noEmit — incremental — watch”,
```

`ts-lint`可以叫任何东西，仅供参考。

这个命令说，*“类型检查代码，但是不要在文件或任何东西中创建类型定义。在我开发“*的时候，也要继续关注代码和类型检查。

`package.json`的`scripts`座现在应该是这样的:

```
"scripts": {
  "build": "next build",
  "dev": "next dev",
  "lint": "next lint",
  ...
  "ts-lint": "tsc --noEmit --incremental --watch",
  ...
},
```

尝试在您的终端中手动运行`ts-lint`。有打字错误吗？搞定他们。

# 添加预提交挂钩

现在让我们建立一个预提交钩子。

第一步，安装`husky` [NPM 包](https://www.npmjs.com/package/husky)作为你的应用程序的开发依赖。

```
npm install -D husky// or via yarn
yarn add -D husky
```

Husky 是一个轻量级的助手，可以与提交工作流结合在一起。

我们来做一个哈士奇一旦安装后的快速配置。更多细节或手动配置，请查看文档。哦，在运行下面的命令之前，确保您的`package.json`文件已经保存。

根据您使用的是`npm`还是`yarn`，这里有一段来自`husky`文档的关于如何运行自动化配置的片段:

```
# NPM
npx husky-init && npm install# Yarn 1
npx husky-init && yarn# Yarn 2
yarn dlx husky-init --yarn2 && yarn
```

运行这个`husky-init`配置脚本做了几件事:

1.  修改您的`package.json`文件，将`husky`添加到您的`scripts`块中，这允许它的执行。
2.  在您的项目根目录下创建一个`.husky`目录，其中包含您想要运行的预提交钩子。您也可以(我们也将)编辑它。

默认情况下，自动 husky 配置创建命令`npm run test`。对于本文的例子，让我们将`npm run test`改为对我们的代码进行类型检查。

# 添加预提交命令

现在将下面的新命令添加到我们的`package.json`文件`scripts`块中。它看起来与上面的`ts-lint`命令非常相似，除了这个命令不监视我们的代码。一次搞定。

```
"ts-lint-commit-hook": "tsc --noEmit --incremental",
```

现在打开项目中的`.husky/pre-commit`文件，让我们更新`husky`的预提交命令:

```
#!*/bin/sh* . "$(dirname "$0")/_/husky.sh"// OLD
*# npm run test**// NEW
npm run ts-lint-commit-hook*
```

仅此而已。现在，随着每次提交，您的 TypeScript 代码将进行类型检查，以确保在您的代码进入任何 CI 工作流之前，它不包含任何类型错误。如果失败了，你会比你的队友更早知道。😁

看看我们正在为西北图书馆知识库构建的一个新的数字收藏应用程序中的[工作实现](https://github.com/nulib/dc-nextjs)，它使用 Next.js、 [Radix](https://www.radix-ui.com/) 、 [Stitches](https://stitches.dev/) ，以及我们正在构建的一个[新设计系统](https://github.com/nulib/design-system)。

[](https://github.com/nulib/dc-nextjs) [## GitHub-nulib/DC-NextJS:NextJS 数字收藏的游乐场

### 运行开发服务器:用浏览器打开 http://localhost:3000。您可以通过修改…开始编辑页面

github.com](https://github.com/nulib/dc-nextjs) 

# Next.js 功能强大

Next.js 是一个强大的下一代平台，用于构建基于 React 的项目。结合通过 TypeScript 中的类型检查减少错误，您可以构建任何东西，从静态单页应用程序、组件库、节点 API 到混合服务器端呈现的应用程序，即使没有数百万页也有数千页。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*

## 进一步阅读

[](/typescript-made-easy-a-guide-to-your-first-type-safe-app-with-next-js-wundergraph-and-prisma-e197a59e2b30) [## 轻松编写类型脚本:使用 Next.js、WunderGraph 和 Prisma 编写第一个类型安全应用程序的指南

### 是时候抛开恐惧，学习 TypeScript 了。让我们给你第一次“发现！”瞬间通过建立一个完整的…

javascript.plainenglish.io](/typescript-made-easy-a-guide-to-your-first-type-safe-app-with-next-js-wundergraph-and-prisma-e197a59e2b30)