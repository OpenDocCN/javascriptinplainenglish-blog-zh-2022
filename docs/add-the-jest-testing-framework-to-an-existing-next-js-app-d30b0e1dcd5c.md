# 将 Jest 测试框架添加到现有的 Next.js 应用程序

> 原文：<https://javascript.plainenglish.io/add-the-jest-testing-framework-to-an-existing-next-js-app-d30b0e1dcd5c?source=collection_archive---------6----------------------->

## 找到将 Jest 添加到 Next.js 应用程序的简单方法。

![](img/f67dd8e2f13bbf4164809ccdf8bd8ada.png)

*原发布于*[*https://fek . io*](https://fek.io/blog/add-jest-testing-framework-to-an-existing-next-js-app)*。*

我一直在用 [Next.js](https://nextjs.org/) 做我目前正在做的一个新项目。我在 Node.js 上使用 web 应用程序的大部分经验都是使用 [Express.js](https://expressjs.com/) 框架。我喜欢在测试中使用的工具之一是 [Jest](https://jestjs.io/) 。

如果你还没有机会使用 Jest，它绝对值得一试。它在 React 社区中非常受欢迎，并且在框架中内置了测试覆盖。

# 将 Jest 添加到 Next.js 的简单方法

将 Jest 添加到 Next.js 的最简单方法是在使用`create-next-app`命令行工具搭建一个新应用时这样做。以下是如何使用该工具创建下一个应用程序的示例:

```
npx create-next-app --example with-jest with-jest-app 
# or 
yarn create next-app --example with-jest with-jest-app 
# or 
pnpm create next-app -- --example with-jest with-jest-app
```

这将创建一个示例 Next.js 应用程序，其中 Jest 已经配置好并准备就绪。

# 向 Next.js 添加 Jest 并不难

如果你有一个预先存在的 Next.js 应用程序，jest 可以很容易地添加。我们将通过以下步骤向 Next.js 12 应用程序添加 Jest

# 添加测试模块

使用您选择的软件包管理器添加`@testing-library/react`、`@testing-library/jest-dom`、`jest-environment-jsdom`模块。我将使用`yarn`作为我的例子:

```
yarn add jest @testing-library/react @testing-library/jest-dom jest-environment-jsdom --dev
```

# 添加 Jest 配置

我们需要做的下一件事是向我们项目的根目录添加一个`jest.config.js`文件，并编写以下配置代码:

# 添加单元测试

现在，我们将为登录页面添加第一个单元测试。我们将在根目录下为我们所有的测试创建一个文件夹。Jest 使用下面的`__tests__`目录来存储所有的 Jest 测试。我们将创建这个目录，并为我们的测试添加一个名为`index.test.js`的测试文件。将以下代码添加到该文件中:

# 向 package.json 添加一个测试运行程序

我们的最后一步是修改我们的`package.json`文件，向脚本部分添加一个测试运行程序脚本。我的脚本部分如下例所示:

```
...
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "test": "jest"
  },
...
```

# 运行我们的单元测试

现在我们已经完成了这四项更改，我们可以运行第一个测试了:

```
> yarn test
yarn run v1.22.18
$ jest
 PASS  __tests__/index.test.js
  Home
    ✓ renders a heading (94 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.419 s
Ran all test suites.
✨  Done in 3.29s.
```

现在，如果我们想要添加一个测试覆盖报告，我们可以在我们的`package.json`文件的脚本部分的测试命令中添加`--coverage`标志。

```
"test": "jest --coverage"
```

如果您再次运行测试运行程序，您的输出应该如下所示:

```
❯ yarn test
yarn run v1.22.18
$ jest --coverage
 PASS  __tests__/index.test.js
  Home
    ✓ renders a heading (90 ms)

----------|---------|----------|---------|---------|-------------------
File      | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
----------|---------|----------|---------|---------|-------------------
All files |     100 |      100 |     100 |     100 |
 index.js |     100 |      100 |     100 |     100 |
----------|---------|----------|---------|---------|-------------------
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.382 s
Ran all test suites.
✨  Done in 3.13s.
```

# 结论

在测试和模仿方面，Next.js 提供了很多选项。除了 Jest，你还可以使用[柏树](https://docs.cypress.io/guides/getting-started/writing-your-first-test#What-you-ll-learn)、[剧作家](https://playwright.dev/docs/intro)或[维特斯特](https://github.com/vitest-dev/vitest)进行测试。

在这篇文章中使用 Jest 的例子是使用 Rust 编译器，但是如果你愿意，你也可以使用 Babel 来运行 Jest。祝测试愉快！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***