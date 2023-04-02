# 如何在 2022 年创建 NodeJS & TypeScript 样板文件

> 原文：<https://javascript.plainenglish.io/how-to-create-a-node-js-typescript-boilerplate-in-2022-783f6e15c17a?source=collection_archive---------6----------------------->

## 创建 Node.js & TypeScript 样板文件的指南，具有简单的配置和热重装支持

![](img/f19e3823d8d934d82e0773690e2b7474.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

从头开始创建 Node.js 项目通常是我们不经常做的事情。但是作为一名高级软件工程师，了解后端的一切是非常重要的。

让我们通过用 TypeScript 创建一个样板 Node.js 项目来学习。此外，了解我们如何使用 TypeScript 添加开发模式！

我们将从两个方面着手。

## 在我们开始之前…

我用 ExpressJS 和 Typescript 创建了一个[专业样板。本文是这个系列的一部分。你可以在下面找到所有的文章。](https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate)

```
***** [**Creating a ExpressJS + Typescript Boilerplate**](/create-an-express-boilerplate-with-typescript-810eb6c29196) ***** [**How to setup Linter and Formatter for NodeJS**](/how-to-set-up-linter-formatter-for-node-js-d6b34c0c8be5) ***** [**How to handle multiple environments in NodeJS**](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) ***** [**Error Handling in NodeJS**](/error-handling-in-node-js-like-a-pro-ed210baa0600) ***** [**Request Validation in NodeJS**](https://medium.com/p/c69f2494cf18) ***** [**Using Docker Professionally with NodeJS**](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) ***** [**Using Docker for Local Development in NodeJS**](/node-js-database-with-docker-for-local-development-285212c5162f) ***** [**Logging in NodeJS**](/node-js-logging-for-professionals-6be07c003e7f) ***** [**Kubernetes with NodeJS**](https://levelup.gitconnected.com/kubernetes-deployment-with-nodejs-made-easy-eaeec32b62e3)
```

我们开始吧！

## **第一步:创建一个新项目**

首先，为您的项目创建一个新目录。

```
mkdir nodejs-typescript-skeletoncd nodejs-typescript-skeleton
```

## **步骤 2:初始化 npm 项目**

然后运行下面的命令，用 yarn 初始化项目。如果你愿意，你可以使用 npm。这没什么不同。

```
yarn init -y
```

## **步骤 3:为我们的项目创建一个条目**

然后创建一个名为“src”的新文件夹，并在其中创建一个名为 **index.js** 的新文件。

将以下代码直接粘贴到该文件中:

```
const name = ‘faisal’console.log(‘this is working’);
```

现在从控制台运行该项目，看看它是否正常工作:

```
node src/index.js
```

它将打印消息，这意味着我们的项目启动并运行。

## **第四步:我们来介绍一下打字稿**

但我们不再活在过去了，对吗？我们不再需要 JavaScript 了。所以让我们把文件转换成 TypeScript。

将我们的`index.js`文件重命名为`index.ts`。

然后在本地安装 TypeScript(作为一个开发依赖项)。

```
yarn add -D typescript
```

现在我们有了 TypeScript，这很棒，但它不知道如何正常工作。为此，我们需要一个配置文件。

让我们在名为`tsconfig.json`的根文件夹中创建一个 TypeScript 配置文件。并将以下代码粘贴到那里:

tsconfig.json

注意，在第 2 行，我们扩展了一个基本配置。它为`node16`提供了一些合理的默认值。

为了使用它，我们需要先安装它。

```
yarn add -D @tsconfig/node16
```

同样的配置[也可用于其他 Node.js 版本](https://github.com/tsconfig/bases)

首先，我们将`*outDir*`配置为`dist`，这意味着我们的捆绑文件将进入一个名为`dist`的新目录

3.我们只指定要编译的`src`文件夹。所以我们所有的打字稿文件都会放在那里。

4.我们从编译中排除了`node_modules`文件夹，以避免问题并缩短构建时间。

最后，让我们通过运行以下命令来包含 Node.js 的类型定义:

```
yarn add -D @types/node
```

## **第五步:我们来编译**

所以现在我们已经设置了 TypeScript。但是我们的浏览器或者 Node.js 对 TypeScript 一无所知。他们只懂 JavaScript，对吗？

所以我们需要做的是将我们的类型脚本文件转换成 JavaScript。这个过程叫做编译。

就这么办吧。

```
yarn tsc
```

现在进入你的`dist`文件夹查看编译后的文件。您将在那里看到一个 JavaScript 版本的`index.ts`文件！

然后通过运行以下命令来执行您的代码:

```
node dist/index.js
```

然后嘣！你的代码运行良好。

## **第六步:直接执行一个类型脚本文件**

在运行我们的应用程序之前运行`tsc`命令是不实际的。我们需要一种方法来自动化这个过程。

而且有解决这个问题的套餐！让我们补充一下！

```
yarn add -D ts-node
```

现在`[ts-node](https://www.npmjs.com/package/ts-node)`是一个可以用来直接运行任何 TypeScript 文件的包。所以我们先试试。

```
ts-node src/index.ts
```

它将直接执行 TypeScript Node.js 文件。不需要编译！这一切都会自动发生。

## **第七步:开发模式**

现在我们可以直接运行一个 TypeScript 文件，而不用编译成 JavaScript。让我们更进一步。

在开发期间，我们需要对项目的热重装支持。

让我们添加一个流行的包来解决这个问题:

```
yarn add -D nodemon
```

[Nodemon](https://www.npmjs.com/package/nodemon) 是一个可以在你保存文件时观察文件变化并编译它们的包，这样你就不用一次又一次的运行文件了。

让我们试着运行一下:

```
yarn nodemon src/index.ts
```

现在，继续在您的`index.ts`文件中进行更改，以查看实时更改。

## **奖励步骤:让开发变得更加愉快**

还有一个专门为 TypeScript 项目制作的包。其`[ts-node-dev](https://www.npmjs.com/package/ts-node-dev)`包。

让我们将它添加到项目中，看看我们能做些什么:

```
yarn remove nodemon ts-node // ->remove the previous 2 packagesyarn add -D ts-node-dev // -> add the new one!
```

现在，让我们运行以下命令，看看它是否能按预期工作:

```
yarn ts-node-dev -respawn src/index.ts
```

请注意，`-respawn`标志用于确保文件在更改时被重新编译。

当您使用 TypeScript 时，“ts-node-dev”比“nodemon”更好。而且速度也更快。

## **最终改进:添加脚本**

现在转到您的`package.json`文件，添加下面的脚本使它更简单。

package.json

然后，您可以运行下面的命令让它在开发模式下运行:

```
yarn dev
```

要构建项目，只需运行以下命令:

```
yarn build
```

现在您有了一个可工作的 Node.js 框架项目！你可以用任何你喜欢的方式使用它。

今天到此为止！我希望你学到了新的东西！祝你愉快，:D

**Github 回购:**

[](https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton) [## GitHub-Mohammad-fais al/nodejs-typescript-skeleton:这是一个使用 nodejs 和…

### 这是一个使用 nodejs 和 typescript-GitHub-Mohammad-fais al/nodejs-typescript-skeleton 的骨架项目:这是一个…

github.com](https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***