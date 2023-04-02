# 如何在 React 或 Next.js 项目中设置 ESLint 和 beautiful

> 原文：<https://javascript.plainenglish.io/how-to-set-up-eslint-and-prettier-in-react-or-next-js-246eb33a1405?source=collection_archive---------0----------------------->

## 用 VS 代码自动格式化代码

![](img/9e10ec623a3aa1571b7d64ca3b19f1b8.png)

Photo by [alwi hafizh Almumtaz](https://unsplash.com/@alwihafizh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

ESLint 让我们可以轻松地捕捉 React 或 Next.js 项目中的错误和不良实践。

更漂亮的让我们通过遵循一些定义好的规则来自动格式化我们的代码。

在本文中，我们将了解如何在 React 或 Next.js 项目中设置 ESLint 和 appearliet，并在 VS 代码中使用 appearliet 在保存时自动格式化代码。

# 入门指南

首先，我们必须在 React 或 Next.js 项目中安装几个包。

要安装所有这些组件，我们运行:

```
npm i -D babel-eslint eslint eslint-config-airbnb eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks prettier
```

`-D`标志将把包作为开发依赖项安装。

然后在 VS 代码中，我们安装 ESLint 和更漂亮的扩展。

最简单的方法是按 Ctrl+Shift+P，然后在命令搜索框中搜索“安装扩展”。

然后在左侧的扩展窗格中输入扩展的名称。

现在我们可以配置 ESLint 和 Prettier 来搜索问题和格式化我们的代码。

# 配置 ESLint

要配置 ESLint，我们可以在项目文件夹的根目录下添加一个`.eslintrc.json`文件，并添加:

```
{
  "root": true,
  "parser": "babel-eslint",
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:import/errors",
    "plugin:import/warnings",
    "plugin:react-hooks/recommended",
    "airbnb-base",
    "airbnb-base/rules/strict",
    "airbnb/rules/react",
    "plugin:prettier/recommended"
  ],
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true,
    "node": true
  },
  "parserOptions": {
    "ecmaVersion": 2021,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "plugins": [],
  "rules": {
    "react/react-in-jsx-scope": "off",
    "react/jsx-props-no-spreading": "off",
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [
          ".js",
          ".jsx"
        ]
      }
    ],
    "prettier/prettier": [
      "error",
      {},
      {
        "usePrettierrc": true
      }
    ]
  }
}
```

我们扩展了希望 ESLint 在`extends`部分检查的规则集。

在`rules`部分，我们配置或关闭一些规则。

`'off'`把它们关掉。

其余的规则设置为默认值。

`ecmaVersion`设置为 2021，检查截至 2021 年的最新 JavaScript 语法。

# 配置更漂亮

为了配置得更漂亮，我们在项目文件夹根目录下创建一个`.prettierc`文件，并添加:

```
{
  "semi": true,
  "tabWidth": 2,
  "printWidth": 100,
  "trailingComma": "all",
  "jsxBracketSameLine": true
}
```

我们添加了一些规则，使代码按照我们想要的方式格式化。

`printWidth`设置最大线宽。

让 beauty 在允许的地方添加尾随逗号。

在应该有分号的地方添加分号，比如行尾。

`tabWidth`根据空格设置标签的宽度。2 表示制表符有两个空格。

`jsxBracketSameLine`将多行 JSX 元素的右括号放在最后一行的末尾，而不是下一行。

此外，我们需要确保更漂亮地格式化我们编写的代码文件，而不是包或自动生成的文件。

为此，我们向项目文件夹根目录添加一个`.prettierignore`文件，并编写:

```
.next
node_modules
.vscode
package.json
package-lock.json
dist
```

`.next`是包含已构建文件的 Next.js 特定文件夹。

`dist`已建文件。

`.vscode`有 VS 工作区的代码设置。

# 配置 VS 代码在保存时格式化文件，并自动修复 ESLint 问题

为了用更漂亮的格式格式化代码，并修复可以自动修复的 ESLint 问题，我们将以下内容添加到`.vscode/settings.json`:

```
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "editor.formatOnSave": true,
  "eslint.alwaysShowStatus": true
}
```

我们可以通过按 Ctrl+Shift+P 将默认格式化程序设置为更漂亮，然后搜索“格式文档”,按 Enter，然后选择“配置默认格式化程序”,然后我们可以选择更漂亮。

# 结论

我们可以修复 React 和 Next.js 项目中的许多代码问题，用 ESLint 让我们的代码更整洁、更漂亮。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*