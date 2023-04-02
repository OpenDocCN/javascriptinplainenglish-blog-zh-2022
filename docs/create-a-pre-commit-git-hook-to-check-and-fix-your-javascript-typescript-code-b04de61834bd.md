# 创建一个预提交 Git 挂钩来自动检查和修复您的 JavaScript/TypeScript 代码

> 原文：<https://javascript.plainenglish.io/create-a-pre-commit-git-hook-to-check-and-fix-your-javascript-typescript-code-b04de61834bd?source=collection_archive---------0----------------------->

## 使用 ESLint、Prettier、lint-staged 和 Husky 提高代码质量

![](img/08ae9b5c15f8563146e1fbb6dc465eb7.png)

Photo by Vishal Jadhav from [Unsplash](https://unsplash.com/photos/xBmmFz2psKw).

在一个项目中有一个统一的编码风格是很重要的，特别是对于一个 JavaScript/TypeScript 项目。这是因为 JavaScript 是一种非常灵活的语言，而 TypeScript 在语法上不太灵活，但在格式上仍然非常灵活。假设代码的某一部分使用 2 个空格进行缩进，而另一部分使用 4 个空格。嗯，你可能会认为这样的林挺只是装饰性的(我不同意)，linters 也可以检查语法，并帮助你用通用的行业标准提高代码质量。

手工检查代码质量和编码风格很麻烦。幸运的是，有了 Git 钩子，它可以自动完成，如果林挺不能被传递，作者将不能创建提交。对于 JavaScript/TypeScript 项目，有一些成熟的包可用于林挺和管理 Git 挂钩。在这篇文章中，我们将介绍如何使用 **ESLint** 、**beauty**、 **lint-staged** 和 **Husky** 创建一个 Git 预提交钩子来检查 JavaScript/TypeScript 代码。

## 安装和配置 ESLint

ESLint 比本文中使用的其他软件包更复杂。建议先查看[这篇文章](https://lynn-kwong.medium.com/use-eslint-to-make-your-javascript-typesript-code-more-professional-1170bbdff32b)找 ESLint，特别是如果你想用它来检查 TypeScript 代码的话。那个帖子可以帮你解决你为项目设置 ESLint 时的各种问题。

如果您只想快速设置 ESLint，可以运行此命令，使用向导安装和配置 ESLint:

```
$ **npm init** [**@eslint/config**](http://twitter.com/eslint/config)
```

选择最适合您项目的选项，`package.json`文件将相应更新。将根据您的选择自动创建一个`[*.eslintrc.js*](https://gist.github.com/lynnkwong/a3300c1b8e0a38348a619bfafcb6812d#file-1170bbdff32b-eslintrc-1-js)`文件。你需要做一些改变来满足你的需求。这是将在这篇文章中使用的`[*.eslintrc.js*](https://gist.github.com/lynnkwong/a3300c1b8e0a38348a619bfafcb6812d#file-1170bbdff32b-eslintrc-1-js)`文件。更多细节可以在 [ESLint 帖子](https://lynn-kwong.medium.com/use-eslint-to-make-your-javascript-typesript-code-more-professional-1170bbdff32b)中找到。

## 安装和配置更漂亮

如果您的项目只有 JavaScript 和 TypeScript 代码，ESLint 通常就足够了，因为它可以执行语法和格式检查。然而，如果你的项目也有 HTML 和 CSS 文件，你也需要安装一个专门的代码格式化工具[。此外，由于大多数 ide 中都有 pretty(比如](https://github.com/prettier/prettier) [VS Code](https://levelup.gitconnected.com/some-tips-to-make-your-vs-code-more-efficient-db77ec7071f8) )，所以使用 pretty 比 ESLint 更便于自动格式化代码。

运行以下命令来安装更漂亮的:

请注意，除了更漂亮的包之外，还安装了两个 ESLint 包，因此它可以很好地与 ESLint 一起工作，因为这两个包在代码格式化方面有一些重叠。

大多数情况下,“更漂亮”的默认设置已经足够了。但是，如果您的项目需要一些特殊的样式，您可以将它们添加到项目根文件夹中一个名为`.prettierrc.json`的文件中。如果选项不太多，可以直接在命令行上添加。检查[此链接](https://prettier.io/docs/en/options.html)了解所有更漂亮的格式选项。

## 安装和配置 lint-staged

默认情况下，像 ESLint 和 Prettier 这样的 linters 会检查项目中的所有文件。然而，这是非常低效的。当创建提交时，我们只希望 linters 检查被更改或暂存的文件。文件被暂存意味着您已经运行`git add`将其添加到[暂存区](https://lynn-kwong.medium.com/understand-different-git-states-and-the-corresponding-file-states-fc62348e81d7)。这就是 *lint-staged* 包的亮点，它让我们只 lint 被暂存的文件。

要安装 *lint-staged* ，运行以下命令:

```
$ **npm install --save-dev lint-staged**
```

要配置 *lint-staged* ，您可以在`package.json`中创建一个名为`lint-staged`的新对象，或者在项目文件夹中创建一个名为`[.lintstagedrc.json](https://github.com/okonet/lint-staged#configuration)`的新文件。如果您有复杂的设置，后者更好。但是，我们将使用前者，因为只有少数设置:

这里我们为 *lint-staged* 定义三个任务。默认情况下， *lint-staged* 将同时运行任务[和](https://github.com/okonet/lint-staged#task-concurrency)。所以，如果同一个文件被不同的任务修改，就要格外注意了。由于比赛条件，结果可能是不可预测的。我们应该确保不同棉条的设置没有冲突。如果有必要，我们可以通过在命令行上为`lint-staged`使用`--concurrent false`来禁用并发性:

```
# Run the tasks concurrently:
$ **npx lint-staged**# Run the tasks sequentially:
$ **npx lint-staged --concurrent false**
```

请注意，当一个任务失败时，所有其他任务都将被跳过或终止。

## 安装和配置 Husky

上面我们用`npx`手动运行了*皮棉暂存*。如果我们想在创建提交之前实施林挺，我们应该在[预提交 Git 挂钩](https://lynn-kwong.medium.com/use-pre-commit-commit-msg-and-pre-push-git-hooks-to-fix-your-python-code-asap-77d80d3ce412)中运行 *lint-staged* 。预提交挂钩实际上只是一个在提交创建之前运行的可运行脚本。在预提交钩子中我们可以有任何代码，林挺代码是一个完美的用例。

有三种方法可以为预提交钩子中的 *lint-staged* 添加林挺代码:

*   [手动创建一个预提交钩子](https://lynn-kwong.medium.com/use-pre-commit-commit-msg-and-pre-push-git-hooks-to-fix-your-python-code-asap-77d80d3ce412)并添加上面的命令来运行其中的 *lint-staged* 。这有点麻烦，因为您需要手动将预提交钩子复制到`.git/hooks/`文件夹。
*   使用[预提交安装程序](https://github.com/observing/pre-commit)。如果我们只有预提交钩子，而没有其他类型的 Git 钩子，比如 *commit-msg* 或 *pre-push* ，这就很方便了。
*   使用[哈士奇](https://typicode.github.io/husky/#/)！Husky 支持所有的 Git 挂钩。这是目前在 JavaScript/TypeScript 项目中管理 Git 挂钩最流行的方法，并将在本文中使用。

要安装 *husky* 并使用 *husky* 初始化项目，运行以下命令:

```
$ **npx husky-init && npm install**
```

一个名为`.husky`的新文件夹将在您的项目文件夹中创建，其中包括一个带有下划线“`_`”的特殊文件夹和一个模板*预提交*钩子。此外，`package.json`中增加了一个名为`prepare`的新脚本，运行`husky install`命令。`[prepare](https://docs.npmjs.com/cli/v8/using-npm/scripts#life-cycle-scripts)` [脚本](https://docs.npmjs.com/cli/v8/using-npm/scripts#life-cycle-scripts)会在打包之前创建`.husky`文件夹。

让我们在`.husky`文件夹的预提交钩子中添加运行 *lint-staged* 的命令:

这个预提交挂钩将在您在当前项目中创建提交之前被调用。我们还需要将它添加到项目文件夹中，这样当它被推送到远程存储库时，它将在项目中保持不变。不用担心，不会被`husky install`命令覆盖。

```
$ **git add package.json**
$ **git add package-lock.json** $ **git add .husky/pre-commit** $ **git commit**
```

现在，当您试图为一个文件创建一个与上面所示的 *lint-staged* 定义的模式相匹配的提交时，预提交钩子将被自动调用。并且只检查暂存文件:

干杯！我们现在已经在项目中成功地建立了一个 Git 预提交挂钩，它为这个项目强制执行了一个编码和格式化标准。现在，如果有人试图添加违反 linters 定义的规则的文件，他/她将无法提交。一开始你可能会讨厌它，但随着时间的推移，你会爱上它，尤其是当你的团队中有一些新成员还不知道你的团队的编码风格时。这将使你的代码库不容易出错，更容易维护，阅读起来更愉快。

帖子里介绍的所有代码都可以在[这个回购](https://github.com/lynnkwong/js-ts-git-hooks)里找到。

## 相关文章:

*   [使用 ESLint 让你的 JavaScript/typescript 代码更加专业](https://lynn-kwong.medium.com/use-eslint-to-make-your-javascript-typesript-code-more-professional-1170bbdff32b)
*   [使用预提交、提交消息和预推送 git 挂钩尽快修复您的 Python 代码](https://lynn-kwong.medium.com/use-pre-commit-commit-msg-and-pre-push-git-hooks-to-fix-your-python-code-asap-77d80d3ce412)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****