# 使用 Jest、SuperTest、TypeScript 和 Husky 完成 Node.js 测试设置

> 原文：<https://javascript.plainenglish.io/complete-node-js-testing-setup-with-jest-supertest-typescript-and-husky-e9d3fa109e1d?source=collection_archive---------2----------------------->

## 创建令人惊叹的测试环境的 6 个步骤。无痛苦！

![](img/e509abc6178807962884a6f71b562847.png)

Photo by [Brooke Cagle](https://unsplash.com/@brookecagle?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/happy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 前戏

如果您使用的是 TypeScript，建立一个干净的测试环境总是一件痛苦的事情，

你不能下载 Jest 就开始黑客攻击，你需要配置测试设置，将 ts 文件映射到 js 版本，让 ESLint 停止对你大喊大叫，这样的例子不胜枚举。

但现在不是了！在本文中，我们将通过 6 个步骤来创建一个令人惊奇的测试环境，没有痛苦！

你是不是太激动了，等不及我们走完整个过程，就直接跳到重点上吧！

1.  什么是 Jest、SuperTest 和 Husky？
2.  [安装包并向包中添加脚本](#9e9d)
3.  [设置 jest.config.ts](#8b51)
4.  [为全局 Jest 变量设置 Eslint 插件](#a0f2)
5.  [以单一模式启动 Express Server](#d972)
6.  [配置 Husky 以保护我们的提交历史记录](#fff1)

我们开始吧！🚀

# 1.什么是 Jest、SuperTest 和 Husky？

为了测试我们的代码，我们需要运行测试的特殊软件，你可能会说 Bar，但是你在说什么呢？我们的代码已经在一个环境中运行了，难道我们不能使用它吗？

不，我的朋友，不幸的是，我们不能，为了测试的健康，我们的测试环境必须被分开，在这个新的环境中，我们将模拟其他的包，检查函数调用和做许多其他很酷的事情。

js，ts 的默认测试运行程序是 **Jest** 现在，它是由脸书开发的，它使测试变得非常简单。

SuperTest 是一个允许我们进行高级 HTTP 断言的库，我们可以通过直接发送请求和检查响应来测试 API 端点。你可以把它想象成后端的**再测试库**😂

Husky 是一个在 git 函数执行自身之前运行的库，例如，我们可以在提交或向 GitHub 推送代码之前测试和 lint 我们的源代码。

它使用了 Git 钩子，通过简单的设置提高了代码质量和提交历史。

# 2.安装包并将脚本添加到包中

好了，聊够了！让我们把手弄脏吧。

为了在有限的时间内尽可能多地介绍，我假设您已经有了一个配置了 TypeScript 编译器选项的简单 express 应用程序。

我们有几个包可以将 Jest 与 TypeScript 一起使用:

```
npm i -D jest ts-jest supertest @types/jest @types/supertest
```

我们需要向我们的 package.json 添加一个测试脚本

package.json

```
"scripts": {     
  "test": "jest --coverage", 
},
```

我们添加了一个**覆盖率**标志，以覆盖我们源代码中所有测试的整体覆盖率。

现在，如果您运行这个脚本，它将不会像我们想要的那样运行，因为我们还没有配置 Jest😆！

让我们在下一节做这件事。

# 3.设置 jest.config.ts

我们需要配置我们的 Jest 用法，我们可以简单地使用 Jest 库的 CLI 进行配置。

```
npx ts-jest config:initornpx jest --init
```

我们将使用 Jest 的 CLI，但我们也可以使用 ts-jest 的 CLI，在选择 TypeScript 后，它会自动为我们创建一个 jest.config.ts 文件，有一个默认的模板是很好的，但我们需要更改许多东西来使这个宝贝如我们所愿地运行

这里最重要的是将 **ts-jest** 设置为预设，并将测试环境设置为**节点**

我们必须将预置设置为 ts-jest，因为我们在测试文件中使用 TypeScript，并且我们需要有人在中间使用。对其 JavaScript 编译版本的 ts 扩展

# 4.为全局 Jest 变量设置 ESLint 插件

如果不使用 ESLint，完全可以跳过这一部分，

对于我们这些不得不听 ESLint 叫嚷的人来说，我们需要为 ESLint 接受一些全局变量做一些改变。

默认情况下，当我们使用 Jest 时，我们的代码库周围都有一些全局变量，例如，**描述**和 **it** ，我们不必导入它们来使用它们。

但是你猜怎么着？埃斯林对此一无所知😄谢天谢地，我们有插件来堵住 ESLint 的嘴。

```
npm i -D eslint-plugin-jest
```

我们需要在. eslintrc.json 文件(我们配置 ESLint 的地方)中做两个小的改动

我们添加了 **Jest** 作为插件，我们还将 Jest globals 添加到 env 代码块中。

# 5.以单一模式启动 Express Server

我不想吓到你们，但这是最复杂的部分😂

但是别担心，你的老朋友巴在这里掩护你，🦸🏻‍♂️

SuperTest 希望我们将 express application 作为参数传递，以便工作。

大概直到现在，你都是这样在全局范围内创建 app 的

```
const app = express();
```

嗯，我们不能再像这样启动我们的应用程序了，我们需要使用 app 作为一个 **singleton** 实例，无论我们调用它多少次，它都会返回相同的应用程序。

Singleton 是一种设计模式，无论你调用多少次，它都会返回相同的对象，我们需要它，因为每次运行测试时，我们都不想创建新的 express 应用程序！

为了了解如何创建单例，你可以查看一下[这个](https://refactoring.guru/design-patterns/singleton/typescript/example)惊人的资源(在实现之前，我也查看了它😄)

我们创建一个 Server.js 类，它返回 express 应用程序

现在我们想在 index.ts 中使用它在 http 请求开始时启动服务器

太神奇了！我们刚刚完成了最难的部分，现在让我们来看一个测试示例

您可以创建一个扩展名为 **.test.ts** 的文件，Jest 会自动查找并测试这些文件

我们将创建一个虚拟路由器和虚拟控制器，用于测试目的并编写测试

你可以看到第一个测试是用传统的 Jest 方法进行的，第二个是用 SuperTest 方法进行的。

SuperTest 进行真正高水平的测试，它大大简化了测试过程。

有很多优秀的开源贡献者编写这些解决方案并免费与我们分享，这难道不令人惊讶吗？非常感谢各位，我真的很感激😊

# 6.配置 husky 以保护我们的提交历史

好吧，我们已经能测试狗屎了，为什么我们还需要学习这种沙哑的东西？

你说对了一部分，我的朋友，这一部分是可选的，但 husky 会在你向 git 发送新的 commit 之前进行测试，如果你认为从长远来看，这是一个非常棒的工具，可以保护你的分支！设置起来也很简单，

所以我建议你遵循它，但是如果你说“nahhh”，那么没问题，我的朋友😊

如前所述，在我们执行 git 之前，husky 会执行一些任务(提交、推送等。)

实际上，做一个基本的设置并使用这个伟大的库是非常简单的。

首先，我们从安装依赖项开始

```
npm i -D husky npx husky add .husky/pre-commit "npm test && npm run lint"git add .husky/pre-commit
```

当我们运行这些命令时，我们会在我们的代码库中看到一个新的目录**。哈士奇**

由于这一点，现在每当你发送一个新的提交，首先它将执行所有的测试，它将运行林挺，只有当它通过所有的检查将被提交。

现在，我们的提交历史比以往任何时候都更受保护😁

# 结果

如果你走到这一步，我祝贺你，我的朋友👏我知道阅读一篇技术文章并不是最有趣的事情，但是你证明了你学习新事物的意愿比获得最大的乐趣更重要💪。

在本文中，我们学习了如何在我们的 TypeScript，express 应用程序中正确设置测试。

正如你所看到的，这是一个复杂的多层过程，但是在设置好测试之后，你可以在任何需要的地方轻松地编写你的测试😊

希望我今天能给你展示一些新的东西，祝你测试愉快(尽可能的愉快😂)

# 激励我！

这篇文章花了我几个小时，喝了几杯咖啡才写完😂

如果你从这篇文章中获得了一些价值，请考虑鼓掌👏👏👏和评论😊。

如果你觉得**很慷慨，**甚至可以在社交媒体上分享一些东西？？

请在 Medium 和 Twitter 上关注我，这样你可以收到更多那些甜蜜的内容🍦🍪🍩

在推特上: [@barisbll_dev](https://twitter.com/barisbll_dev) 🔥

下次冒险再见！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***