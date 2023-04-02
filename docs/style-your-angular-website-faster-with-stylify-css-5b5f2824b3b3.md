# 使用 Stylify CSS 更快地设计有棱角的网站

> 原文：<https://javascript.plainenglish.io/style-your-angular-website-faster-with-stylify-css-5b5f2824b3b3?source=collection_archive---------11----------------------->

![](img/a406252dcf529b1e55cbd62623255191.png)

使用 [Stylify CSS](https://stylifycss.com/) 快速轻松地为您的 Angular 应用程序添加风格。为大页面拆分 CSS，或者为整个应用程序创建一个包，得到极小的 CSS。

# 介绍

[Stylify](https://stylifycss.com/) 是一个库，它使用类似 CSS 的选择器根据你写的内容生成优化的实用优先的 CSS。

✨CSS-like 选择器
💎没有学习的框架
💡花在文档上的时间更少
🧰Mangled &极小的 CSS
🤘不需要吹扫
🚀组件、变量、自定义选择器
📦它可以生成多个 CSS 包

# 装置

首先使用 NPM 或纱线安装 [@stylify/bundler](https://dev.to/docs/bundler) 包:

```
npm i -D @stylify/bundler
yarn add -D @stylify/bundler
```

同样对于监视模式，我们需要运行两个并行任务。这可以通过同时使用以下方法来解决:

```
yarn add -D concurrently
npm i concurrently
```

接下来，创建一个文件，例如`stylify.js`:

```
const { Bundler } = require('@stylify/bundler');

const isDev = process.argv[process.argv.length - 1] === '--w';
const bundler = new Bundler({
  watchFiles: isDev,
  // Optional
  compiler: {
    mangleSelectors: !isDev,
    // https://stylifycss.com/docs/stylify/compiler#variables
    variables: {},
    // https://stylifycss.com/docs/stylify/compiler#macros
    macros: {},
    // https://stylifycss.com/docs/stylify/compiler#components
    components: {},
    // ...
  },
});

// This bundles all CSS into one file
// You can configure the Bundler to bundle CSS for each page separately
// See bundler link bellow
bundler.bundle([
    {
        files: ['./src/**/*.html', './src/**/*.ts'],
        outputFile: './src/styles.css',
    },

    // You can also split css for each component
    // You can map files within the components using content comment option
    // https://stylifycss.com/docs/bundler#files-content-option
    // Stylify takes that option and searches for defined files. If defined file
    // also has an option, id check also those files and so long.
    // This way it maps all files and all dependencies.
    /*
    {
        files: ['./src/app/app.component.*'],
        outputFile: './src/app/app.component.css',
    },
    */
])
```

如果你不使用分割，所有的东西都不会打包到`styles.css`中，那么不要忘记添加 css 文件的路径。

最后一步是将脚本添加到`package.json`中:

```
"scripts": {
    "dev": "concurrently 'yarn stylify.dev' 'ng serve -c development'",
    "prod": "yarn stylify.build & ng serve",
    "stylify.build": "node stylify.js",
    "stylify.dev": "node stylify.js --w"
}
```

在生产中，你会得到优化的 CSS 和混乱的 html:

```
<h1 class="font-size:24px color:#dd0031 font-family:arial">
Hello World!
</h1>
```

```
.a{font-size:24px}
.b{color:#dd0031}
.c{font-family:arial}
```

# 斯塔克布利茨游乐场

继续尝试[Stylify CSS+Angular on stack blitz](https://stackblitz.com/edit/stylifycss-angular-example?file=src%2Fapp%2Fapp.component.html)。

# 配置

上面的例子没有包括 Stylify 能做的所有事情:

*   定义[组件](https://stylifycss.com/docs/stylify/compiler#components)
*   添加[自定义选择器](https://stylifycss.com/docs/stylify/compiler#customselectors)
*   配置你自己的宏[像`ml:20px`一样左边距](https://stylifycss.com/docs/stylify/compiler#macros)
*   定义[自定义屏幕](https://stylifycss.com/docs/stylify/compiler#screens)
*   您可以在模板中映射[嵌套文件](https://stylifycss.com/docs/bundler#files-content-option)
*   还有更多

请随意查看文档以了解更多信息💎。

# 让我知道你的想法！

我会很高兴得到任何反馈！ [Stylify](https://stylifycss.com/) 仍然是一个新的库，有很大的改进空间🙂。