# 如何为 Node.js 设置 Linter & Formatter

> 原文：<https://javascript.plainenglish.io/how-to-set-up-linter-formatter-for-node-js-d6b34c0c8be5?source=collection_archive---------6----------------------->

## 自动化您对 ESLint 的使用，与 Husky 一起变得更漂亮

![](img/f19e3823d8d934d82e0773690e2b7474.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/green-technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在 Node.js 项目中拥有 TypeScript 是确保类型安全和改善开发人员体验的一个好方法。但是我们可以通过添加 Linter 和 Formatter 来更进一步。

今天，我们将看到如何使用 TypeScript 向 Node.js 项目添加一个更细更漂亮的元素。

我们从上一篇文章继续这个项目。知识库可在[这里](https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton)找到。

## 在我们开始之前…

我用 ExpressJS 和 Typescript 创建了一个[专业样板。本文是本系列的一部分。你可以找到下面所有的文章。](https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate)

```
***** [**Creating a ExpressJS + Typescript Boilerplate**](/create-an-express-boilerplate-with-typescript-810eb6c29196) ***** [**How to setup Linter and Formatter for NodeJS**](/how-to-set-up-linter-formatter-for-node-js-d6b34c0c8be5) ***** [**How to handle multiple environments in NodeJS**](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) ***** [**Error Handling in NodeJS**](/error-handling-in-node-js-like-a-pro-ed210baa0600) ***** [**Request validation in NodeJS**](https://medium.com/p/c69f2494cf18) ***** [**Using Docker Professionally with NodeJS**](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) ***** [**Using Docker for Local Development in NodeJS**](/node-js-database-with-docker-for-local-development-285212c5162f) ***** [**Logging in NodeJS**](/node-js-logging-for-professionals-6be07c003e7f) ***** [**Kubernetes with NodeJS**](https://levelup.gitconnected.com/kubernetes-deployment-with-nodejs-made-easy-eaeec32b62e3)
```

让我们开始吧！

# 第 1 步:安装所需的依赖项

让我们首先安装所需的依赖项。

```
yarn add -D eslint \
@typescript-eslint/eslint-plugin \
@typescript-eslint/parser
```

默认情况下，ESLint 不支持 typescript，所以我们添加了另外两个包作为开发人员依赖项。

# 第 2 步:创建一个配置文件

现在创建一个新的 ESLint 配置文件。

```
touch .eslintrc
```

并将下面的代码粘贴到那里。

```
{
  "parser": "@typescript-eslint/parser",
  "parserOptions": { "ecmaVersion": "latest", "sourceType": "module" },
  "extends": ["plugin:@typescript-eslint/recommended"],
  "env": {
    "node": true // Enabling Node.js global variables
  },
  "rules": {}
}
```

让我们将 package.json 文件中的两个脚本添加到 lint 中，并轻松格式化。

```
"scripts": {
    "lint": "eslint src/**/*.ts",
    "format": "eslint src/**/*.ts --fix"
}
```

现在，您可以运行以下命令来清理整个项目。

```
yarn lint
```

此外，不要忘记创建一个`.eslintignore`文件，以避免遗漏一些文件夹。因为这可能需要一些时间。

```
.eslintignore
```

把下面的代码放在那里:

```
node_modules
dist
```

# 第 3 步:添加更漂亮的

现在让我们将`prettier`添加到项目中。首先，安装依赖项。

```
yarn add -D prettier
```

然后在根文件夹中创建一个`.prettierrc`文件，并在那里添加以下配置

```
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 120,
  "tabWidth": 2
}
```

现在，这个配置只是我个人的喜好。如果需要，您可以使用您的配置。

此外，您还可以添加一个新的脚本，以便同时在所有文件上运行。

```
"scripts": {
    "pretty": "prettier --write \"src/**/*.ts\""
}
```

对所有文件运行得更漂亮，如下所示:

```
yarn pretty
```

# 第四步:添加哈士奇

所有这些都太棒了。但是我总是忘记运行这些命令。为了确保没有坏代码会被推到源代码中，我们可以使用一个很棒的哈斯基工具。

它会在您尝试提交之前运行，并且可以运行一些运行状况检查。为了更好地理解，让我们首先安装它。

```
yarn add -D husky
```

然后在`package.json`文件中添加一个新的块:

```
"husky": {
    "hooks": {
      "pre-commit": "yarn lint"
    }
}
```

因此，每次您尝试提交更改时，这个预提交钩子将运行，您的代码将自动修复。多酷啊！

# Github 回购:

[](https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton) [## git hub-Mohammad-fais al/nodejs-type script-skyline:这是一个使用 nodejs 和…

### 这是一个使用 nodejs 和 type script-GitHub-Mohammad-fais al/nodejs-type script-skyline 的框架项目

github.com](https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton) 

```
**Want to Connect?**You can reach out to me via [**LinkedIN**](https://www.linkedin.com/in/56faisal/) or my [**Personal Website**](https://www.mohammadfaisal.dev/blog)
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*