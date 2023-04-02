# 如何用 Node.js 创建自己的 CLI

> 原文：<https://javascript.plainenglish.io/how-to-create-your-own-cli-with-node-js-7646a976f8fa?source=collection_archive---------11----------------------->

## 第 2 部分:目录创建、通过文件路径定制模板等等

![](img/5f6723e353a8a98878e110f4b867af99.png)

Photo by [Safar Safarov](https://unsplash.com/@codestorm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

亲爱的读者，又见面了！我假设您是在阅读了**“如何使用 Node.js 创建自己的 CLI”**系列的第一部分后阅读了本文。如果是的话，我很高兴你能来这里。如果没有，我推荐先看完，或者直接在这里抓取初始代码[。](https://codesandbox.io/s/create-project-oweiqo)

在本文中，我们将扩展 CLI 的功能，使其更加强大和方便。

# 序

在本文中，我使用没有突出显示 TypeScript 语法的 gists，但是突出显示了 diff。这是有意的，因为已经编写了很多代码，使用 diff 而不是传统的语法高亮会更容易浏览。

这种方法明显的缺点是复制*不同的*代码，但是有工具可以使这变得更容易。我建议您使用您的 IDE 删除您刚刚将 diff 复制到的文件中的所有`+`字符，然后使用[更漂亮的](https://prettier.io/docs/en/index.html)来格式化代码。

例如，在 Webstorm 中就这么简单:

```
// open replace tool
// paste + into the first input, leave the second input blank, and then click Replace all
⌘+R (Ctrl+R)// format code
⌘+⌥+L (Ctrl+Alt+Shift+L)
```

请注意，项目中没有安装更漂亮的配置，但是有一个更漂亮的配置可用，您可以在这里获得它[。您可能需要](https://codesandbox.io/s/create-project-oweiqo)[配置您的 IDE](https://prettier.io/docs/en/editors.html) 来使用它。

**重要提示:**如果您还没有阅读本系列的第一部分，并且刚刚获得代码，请在继续之前遵循以下步骤:

1.  使用 CLI 源代码切换到目录
2.  安装依赖项
3.  运行`npm run dev`
4.  跑`npm link`

这将允许您在系统的任何地方使用此 CLI。

# 项目概述

这是关于用 Node.js 构建自己的 CLI 的系列文章的第二部分。TL；博士:

1.  您可以使用`create-project`命令引导项目。有一个方便的向导可以帮助您记住我们的 CLI 的功能以及可以配置的选项。
2.  在一个单独的终端中运行 CLI 目录下的`npm run dev`，这样我们写的代码就会被自动编译。

在本文中，我们将扩展 CLI 的功能。最终代码可在[这里](https://codesandbox.io/s/create-project-pt2-ytkvzb)获得。这个项目将在节点 14 和以上。

在本文结束时，您将拥有一个强大的跨平台 CLI，用于创建支持定制模板的项目。

# 新功能

我们应该在 CLI 中添加哪些杀手级功能？我会选择这些:

1.  使 CLI 能够创建目录。将项目目录的创建委托给 CLI 会非常方便。call 参数将用于指定项目的名称，因此我们需要为模板设置另一个标志。
2.  **增加对自定义模板的支持。**自定义模板使创建和重用特定模板变得容易，而无需派生库。
3.  **添加选择到设置** `husky` **。**如果用户决定在项目中初始化 git repo，他可能还想设置 [Husky](https://typicode.github.io/husky/#/) 。

这些功能将使使用我们的 CLI 更加方便。如果你在想别的事情，请随意写下评论！与此同时，我会用这些。我们开始吧！

## 先决条件

先做一点配置调整。在第一篇文章中使用 CLI 时，您可能已经看到了这个错误。

```
(!) Unresolved dependencies
[https://rollupjs.org/guide/en/#warning-treating-module-as-external-dependency](https://rollupjs.org/guide/en/#warning-treating-module-as-external-dependency)
```

那是什么？默认情况下，Rollup 只解析相对导入，而`import chalk from chalk` [等导入被视为外部依赖](https://rollupjs.org/guide/en/#warning-treating-module-as-external-dependency)。警告来自于这种行为的隐含性质。为了摆脱这种情况，您要么需要将它们显式地包含在您的包中，要么将它们标记为外部的。有一个汇总插件[可以做到这一点，所以你不必手动列出它们。让我们安装它。](https://github.com/stevenbenisek/rollup-plugin-auto-external)

```
// inside the project tab
npm i -D rollup-plugin-auto-external
```

之后，稍微调整一下汇总配置。

Marking node_modules imports as external

另外，请注意`typescript`插件的`exclude`选项。如果您已经开始填写模板，它还会抑制一些警告。

## 为项目创建目录并添加模板标志

首先，我们需要创建另一个标志来存储模板，以便我们可以使用之前用作项目名称模板的参数。

Move template from CLI call argument to -t flag

之后，我们需要添加另一个选项`project`来存储调用参数，并在`types.ts`中反映这一点。它不能为空，所以如果它没有被传递，我们必须要求用户指定它，并在提供值后检查它。

Adding a project option and asking the user to enter it if it was not specified

注意`prompt-for-missing-options.ts`中关于`project`选项问题中的`validate`功能。如果值无效，它应该返回`false`，这迫使用户键入不同的内容。有关可能的问题对象字段的更多信息，请参见[查询人文档](https://github.com/SBoudrias/Inquirer.js#questions)。

最后，我们需要添加对`project`选项的支持。这必须是为项目创建目录的另一个任务的参数。让我们为这个任务创建一个函数。

```
// inside the project tab
touch src/utils/create-project-directory.ts
```

现在让我们将目录创建逻辑添加到其中，并在我们的任务运行器中使用它。

Adding a task to create a project directory

请注意，我们已经将`targetDirectory`从`process.cwd()`更改为新创建的项目目录，以便其他任务能够正常工作。

```
// playground directory, e.g. /documents// targetDirectory === created directory /documents/something
create-project something
// template files will be copied to the /documents/something directory, the git repo will be initialized there and dependencies will be installed there// targetDirectory === process.cwd()
create-project something
// template files will be copied here to the /documents directory, same goes for the git repo and dependencies
```

现在，让我们检查一下一切是否正常。运行以下命令。

```
// playground directory, e.g. /documents
create-project
```

应该会提示您缺少参数。

```
? Please type project's name (cannot be empty) dir
? Please choose which project template to use JavaScript
? Initialize a git repository? Yes
? Install packages? (Y/n) Yes
```

之后，您可以切换到项目目录并确保一切都按预期工作:模板文件被复制，git 存储库被初始化，并且包(如果您在`package.json`文件中添加了`dependency`部分)被安装。

## 自定义模板

什么是自定义模板？基本上，这是您的本地机器上包含所需模板的目录的路径。您可以运行以下命令，并期望从指定目录中的模板构建项目。

```
// playground directory, e.g. /documents
create-project -t file:./my-custom-template
```

现在我们有两个支持的模板:JavaScript 和 TypeScript。如何实现对这种`file:`语法的支持？

首先，我们需要为新类型的模板创建一个类型，并扩展模板验证助手，以便能够使用`file:`语法。

Adding type for custom templates

注意 TypeScript [模板文字语法](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html):我们可以使用类似``abc{string}``的表达式来描述以特定字符开头的字符串。`checkTemplateValidity`收到了对模板开始符号的额外检查，`parseArgumentsIntoOptions`收到了关于`file:`模板语法的额外日志。为了避免意外，我们还保留了`file:`模板语法的情况。

其次，我们需要弄清楚我们将从哪里获取模板。如果模板以`file:`开始，我们必须解析给定的路径。否则，一切都应该和以前一样工作。

让我们创建另一个实用函数来获取基于其类型的模板路径。

```
// inside the project tab
touch src/utils/get-template-directory.ts
```

之后，给它添加下面的代码，并在`main.ts`中使用它来得到`templateDirectory`。

Calculating template path based on its type

这里是另一个`startWith`检查，看看我们是否有一个自定义模板。如果是，那么将使用给定的路径，如果不是，我们像以前一样使用一个受支持的模板。

我们试试吧！

创建一个自定义模板目录，并在其中放置一些文件。

```
// playground directory, e.g. /documents
mkdir my-custom-template
touch my-custom-template/index.html
```

现在，让我们使用这个模板来创建一个项目。

```
// playground directory, e.g. /documents
create-project my-project -t file:my-custom-template
```

当提供其他选项时，用`n`键拒绝它们。等待项目创建完成。您应该会看到如下所示的日志。

```
? Initialize a git repository? No
? Install packages? No
  ✔ Create project directory
  ✔ Copy project files
  ↓ Install dependencies [skipped]
    → Pass --install or -i to automatically install dependencies
DONE Project ready
```

转到已创建项目的目录，确保它包含我们使用的定制模板中的`index.html`文件。

太好了！起作用了。但是像往常一样，有一个小问题。运行以下命令:

```
// playground directory, e.g. /documents
create-project my-another-project -t file:my-nonexisted-template
```

跳过提示。您应该会看到这样的日志:

```
? Initialize a git repository? No
? Install packages? No
  ✔ Create project directory
  ✖ Copy project files
    Install dependencies
ERROR Error occurred
```

你注意到什么问题了吗？我们试图使用一个不存在的模板。这没什么不对的，对吧？我们怎么能用不存在的东西呢？让我们尝试使用现有的模板。

```
// playground directory, e.g. /documents
create-project my-another-project -t file:my-custom-template
```

砰！`my-another-project`目录已经创建！

```
? Initialize a git repository? No
? Install packages? No
  ✖ Create project directory
    → mkdir: my-another-project: File exists
    Copy project files
    Install dependencies
```

想象一下，你犯了一个小小的错别字，得到了一个错误，用正确的数据再试一次，但仍然看到错误。不太方便吧？在继续任何任务之前，我们需要检查模板目录。

首先，让我们再创建两个实用程序:

```
// inside the project tab
touch src/utils/get-template.ts
touch src/utils/custom-template-helpers.ts
```

`get-template.ts`将用于从`-t`标志中获取传递的模板或基于原始模板的`undefined`。它也会记录错误，如果有的话，而不是`parse-arguments-into-options.ts`。模板助手，比如检查传递的模板是否是自定义模板，它的路径解析器将存储在`custom-template-helpers.ts`中。

现在让我们在其中编写代码，并将它们与项目挂钩:

Checking custom template before proceeding

代码很多，我们来分解一下。

首先，我们创建了上面的函数。

其次，我们在`parse-arguments-into-options.ts`中使用了`getTemplate`。由于`getTemplate`的异步特性，`parseArgumentsIntoOptions`变成了异步的，所以`cli`正在等待它。

最后，我们重构了`get-template-directory.ts`以使用来自`custom-template-helpers.ts`的助手。

让我们看看这是否解决了我们的问题。删除之前创建的`my-another-project`目录，并尝试使用不存在的模板再次创建项目。

```
// playground directory, e.g. /documents
rm -rf my-another-project
create-project my-another-project -t file:my-nonexistent-template
```

您应该会看到下面的日志:

```
WARNING There is no such template: /path/to-/template/my-nonexistent-template. Check the specified path
```

请停止向导，并使用现有模板重试。

```
// playground directory, e.g. /documents
create-project my-another-project -t file:my-custom-template
? Initialize a git repository? No
? Install packages? No
  ✔ Create project directory
  ✔ Copy project files
  ↓ Install dependencies [skipped]
    → Pass --install or -i to automatically install dependencies
DONE Project ready
```

真见鬼。我们解决了过早创建项目目录的问题，现在我们的 CLI 可以从自定义模板创建项目，正确处理它们并方便地响应可能的错误。

## 强壮的

什么是[哈士奇](https://typicode.github.io/husky/#/)？它是一个在提交或推送时运行某些东西的工具。Husky 使得在提交或推送代码之前运行测试、lint 代码甚至提交消息变得简单。我们不会强制执行特定的操作，但会初始化 Husky 以在提交时运行默认的`npm test`。

首先，让我们添加对另一个选项`-h`的支持。

Adding -h option

请注意，新标志`-h` ( `--husky`)用于执行`-g`和`-i`标志。为什么？

1.  没有 git 就没有使用 Husky 的意义。
2.  [Husky](https://typicode.github.io/husky/#/?id=automatic-recommended)的自动设置需要在`husky-init`之后安装依赖项。

我们还为 Husky 选项添加了一个提示，但只在设置了 git 选项时，无论是通过 call 参数还是提示。当使用提示选择 Husky 选项时，不会提示安装选项设置，并且安装选项的答案值会自动设置为`true`。它为`-h`选项提供了一致的行为，无论是用 call 参数还是提示符指定。

之后，让我们创建另一个 util 来初始化 Husky:

```
// inside the project tab
touch src/utils/init-husky.ts
```

最后，让我们为这个任务编写代码，并在任务运行器中使用它:

Creating and using a Husky task

注意，我使用了`npx`来运行`husky-init`。如果您使用[纱线](https://yarnpkg.com/)或 [pnpm](https://pnpm.io/) ，您必须使用[文档](https://typicode.github.io/husky/#/?id=automatic-recommended)中提到的不同命令。

```
npx husky-init && npm install       # npm
npx husky-init && yarn              # Yarn 1
yarn dlx husky-init --yarn2 && yarn # Yarn 2+
pnpm dlx husky-init && pnpm install # pnpm
```

我有意跳过安装依赖项，因为这是一个已经存在的独立任务。

现在，让我们检查该选项是否被选中并正常工作。运行以下命令。确定您的终端中的日志与下面的匹配:

```
// playground directory, e.g. /documents// 1\. Without -g or -h. Reject prompt for -g
create-project project-name -t javascript
? Initialize a git repository? No
? Install packages? (Y/n)// 2\. Without -g or -h. Accept prompt for -g. Reject prompt for -h
create-project project-name -t javascript
? Initialize a git repository? Yes
? Initialize Husky? No
? Install packages? (Y/n)// 3\. Without -g or -h. Accept prompt for -g. Accept prompt for -h
create-project project-name -t javascript
? Initialize a git repository? Yes
? Initialize Husky? Yes
// There should be no prompt for -i// 4\. With -g. Assume that rejecting/accepting the prompt for -h works the same way as before
create-project project-name -t javascript -g
? Initialize Husky? (y/N)// 5\. With -h
create-project project-name -t javascript -h
// There should be no prompts at all
```

此外，检查哈士奇是真的安装。

```
// playground directory, e.g. /documents
// assume you created a project named project-name
cat project-name/.husky/pre-commit
```

您应该会看到下面的日志。如果是，那么一切都很好。

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"npm test
```

# 结论

我们做得很好！我们现在可以为项目创建目录，使用定制模板，并为 git 项目设置 Husky。我们的 CLI 变得越来越强大和方便。

我还想在这个系列中介绍一些内容，比如发布到 NPM 和 CI/CD。关注并订阅，让你不要错过！

如果你喜欢这篇文章，请告诉我！

祝你今天开心！玩的开心！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*