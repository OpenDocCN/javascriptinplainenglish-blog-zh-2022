# 如何在 60 秒内升级一个 JavaScript 项目中 Yarn 的版本

> 原文：<https://javascript.plainenglish.io/how-to-upgrade-the-version-of-yarn-in-a-javascript-project-in-60-seconds-5905526a00b0?source=collection_archive---------9----------------------->

## 需要在一个 JavaScript 项目中将 Yarn 更新到最新版本？这比你想象的要简单，但是在你开始之前有一些事情你需要知道，尤其是如果升级到 Yarn 3。

![](img/40ea3b9b9b4dc63c7969f4cbea501b90.png)

Photo by [Laårk Boshoff](https://unsplash.com/@laarkstudio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

项目经理`yarn`因为从《经典`yarn`(`v1`)到《现代`yarn`(`v2+`)的重大突破性变化，名声有点不好。

尽管如此，我已经习惯在我所有的项目中使用现代、最新版本的`yarn`，而不是替代版本`npm`。

使用`yarn`的一个好处是它的版本直接绑定到你的项目的 CommonJS 模块中(一个`.cjs`文件)，而不是`node`的版本。

您实际上将当前发布版本的 Yarn 签入您的 Git 库，这意味着升级`yarn`不同于升级`npm`。

在本教程中，您将学习如何将 Yarn 更新到最新版本，这只是比将`npm`更新到最新版本稍微复杂一点。

# 如何将`npm`升级到最新版本

在我们谈论升级`yarn`之前，让我们先介绍一下升级`npm`，这样两种解决方案之间的区别会更清楚一些。

类似于你如何用`node -v`检查你的 Node.js 版本，用`-v`简称`--version`，你可以用`npm -v`检查你的`npm`版本。

然后，要升级`npm`，您可以运行一个简单的`npm update -g`命令，它将获取最新版本的`npm`并在全球范围内安装。

或者，如果你正在升级 Node.js，你将自动获得一个更新版本的`npm`，因为它们是打包在一起的。

正如我们将看到的，Yarn 使用了一组明显不同的命令，您需要将升级版本的`yarn`提交到您的`git`存储库中。

# 如何查看当前版本的 Yarn

您可能认为`yarn version`命令是用来检查`yarn`的当前版本的，但它实际上是用于包版本控制的。

相反，要检查`yarn`的当前版本，你只需要运行带有`-v`标志的 Yarn CLI(命令行界面)(`--version`的简称):

```
yarn -v
```

结果要么是经典纱线(指通过`npm`安装的`yarn`，也称为`v1`，要么是现代纱线(通过`yarn`、`v2+`安装的`yarn`)。

截至本文发布时，`yarn`的最新版本是`3.2.2`，因此我交替使用“现代纱线”和`v3`这两个术语。

# 但是现代纱线没有突破性的变化吗？

嗯，是的，现代`yarn`有突破性的变化。有一本很大的迁移指南，我已经读了好几遍，你可能也需要:

 [## 移民

### 任何主要版本都有其突破性的变化，Yarn 2 也不例外。一些旧的行为被清理，修正…

yarnpkg.com](https://yarnpkg.com/getting-started/migration) 

但是，每次我不得不这样做的时候，将一个简单的 Yarn 项目从`v1`升级到`@latest`就像运行两个命令一样简单:

```
yarn set version stable
yarn
```

第一个命令会将您更新到最新版本，这意味着即使您是从经典 Yarn ( `v1`)开始的，您最终也会得到现代 Yarn ( `v3`)。

如果出于某种原因你不想更新到 modern Yarn，你可以尝试获取最新版本的 classic Yarn，但我不建议这样做:

```
yarn set version classic
yarn
```

如果您正在从经典 Yarn ( `v1`)升级到现代 Yarn ( `v3`)，那么您将看到以下控制台输出，让您知道您正在升级:

```
➤ YN0070: Migrating from Yarn 1; automatically enabling the compatibility node-modules linker 👍
```

第二个命令，`yarn`(你可能记得相当于`yarn install`)，将重新安装你的包并完成版本升级。

在`yarn`命令完成运行后，您需要提交更改，这将包括 Yarn 的最新(升级)版本。

但是在您停止阅读并提交 Yarn 对您的 Git 库所做的所有更改之前，让我们先修复您的`.gitignore`文件。

# 为什么纱线会使我的 PRs 如此嘈杂？

当我使用 modern Yarn 时，看到数百个文件在一个 pull 请求中被更改，我曾经非常恼火，但这实际上是一种额外的好处。

当使用现代纱线默认值时，你选择了一种被称为“[零安装](https://yarnpkg.com/features/zero-installs)”的哲学，我最近成为了它的粉丝。

这个想法是，在你的包注册表关闭的情况下，你仍然可以`yarn install`，因为整个`.yarn/cache`文件夹被提交给`git`。

这意味着`npm`包注册表(或者你公司的 AWS 代码工件)的问题不会阻止你加载整个项目。

您也可以相对安全地将`.yarn/cache`文件夹添加到您的`.gitignore`文件中——您的`yarn install`只需获取整个缓存即可。

只是确保不要把整个`.yarn`文件夹添加到你的`.gitignore`或者`.yarnrc.yml`文件中，因为这些文件决定了你的 Yarn 版本。

# 对于纱线，您应该在`.gitignore`中包含什么？

总结一下，让我们更新一下`.gitignore`文件，因为你需要忽略的是从经典纱线(`v1`)到现代纱线(`v3`)的变化。

(*作者注:*纱的[对](https://yarnpkg.com/getting-started/qa#which-files-should-be-gitignored) `[.gitignore](https://yarnpkg.com/getting-started/qa#which-files-should-be-gitignored)`的推荐可能会有变化。我已经包含了这篇文章发表时的最新信息。)

在这一点上我应该提到，无论您使用的是哪个版本的`yarn`，提交`yarn.lock`文件都被认为是最佳实践。

您提交锁文件(对于`npm`，它是`package-lock.json`文件)的原因是为了记录所有已安装软件包的确切版本号。

如果不提交`yarn.lock`，您的`package.json`文件可能会有不明确的包版本，比如`^4.0.0`或`latest`，它们可能会随着时间而改变。

也就是说，当使用 modern Yarn 时，你需要更新`.gitignore`,因为有新的文件，比如`.yarnrc.yml`配置文件和`yarn`版本。

**如果你正在使用 Yarn 的“零安装”模式**，就像我推荐的那样，那么你需要更新你的`.gitignore`文件，以包含以下几行:

```
# We're using Yarn "Zero Installs"
.yarn/*
!.yarn/cache
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/sdks
!.yarn/versions
```

**如果您没有使用“零安装”**，这意味着您不想将包缓存签入您的 Git 库，那么将它添加到您的`.gitignore`:

```
# We're NOT using Yarn "Zero Installs"
.pnp.*
.yarn/*
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/sdks
!.yarn/versions
```

因此，如果你一直遵循我的非官方“纱线升级指南”，那么你需要做的最后一件事就是`git commit`纱线升级:

```
git commit -a -m "chore: upgrade version of Yarn to latest"
```

实际上，我更喜欢使用 GitHub Desktop 作为`git`的 GUI，但重点是您想要提交更改(并可能打开一个新的 pull 请求)。

**快乐编码！** 🧶🙌🧑‍💻📦🐈

![](img/2bd8ccbdf0a5daa33d8cad8b7be594a1.png)

Photo by [Nasim Keshmiri](https://unsplash.com/@nasimkeshmiri?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

[德里克·奥斯汀博士](https://www.linkedin.com/in/derek-austin/)是《职业规划:如何在 6 个月内成为一名成功的 6 位数程序员 》一书的作者，该书现已在亚马逊上架。