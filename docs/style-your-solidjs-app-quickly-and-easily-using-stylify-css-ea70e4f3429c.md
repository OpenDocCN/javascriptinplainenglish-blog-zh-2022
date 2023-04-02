# 使用 Stylify CSS 快速轻松地设计您的 SolidJS 应用程序

> 原文：<https://javascript.plainenglish.io/style-your-solidjs-app-quickly-and-easily-using-stylify-css-ea70e4f3429c?source=collection_archive---------5----------------------->

![](img/6ca225861c1f963de74ad92c724c5b80.png)

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

使用 cli 安装 Stylify:

```
npm i -D @stylify/unplugin
yarn add -D @stylify/unplugin
```

将以下配置添加到`vite.config.js`:

```
import { defineConfig } from 'vite';
import { stylifyVite } from '@stylify/unplugin';
import solidPlugin from 'vite-plugin-solid';
```

```
const stylifyPlugin = stylifyVite({
    bundles: [{ outputFile: './src/stylify.css', files: ['./src/**/*.jsx'] }],
    // Optional
    compiler: {
        // https://stylifycss.com/docs/stylify/compiler#variables
        variables: {},
        // https://stylifycss.com/docs/stylify/compiler#macros
        macros: {},
        // https://stylifycss.com/docs/stylify/compiler#components
        components: {},
        // ...
    },
});

export default defineConfig({
    plugins: [stylifyPlugin, solidPlugin()],
    server: {
        port: 3000,
    },
    build: {
        target: 'esnext',
    },
});
```

在`src/index.js`中添加 Stylify CSS:

```
import './stylify.css';
```

# 使用

Stylify 语法类似于 CSS。你只要写`_`而不是空格，写`^`而不是引用。

所以如果我们编辑`src/App.jsx`:

```
function App() {
  return (
    <h1 class="font-size:24px margin:12px_24px">
      Hello World!
    </h1>
  );
}
```

在生产中，你会得到优化的 CSS 和混乱的 html:

```
<h1 class="p u">Hello World!</h1>
```

```
.p{font-size: 24px}
.u{margin: 12px 24px}
```

# 斯塔克布利茨游乐场

继续尝试[Stylify CSS+SolidJS on stack blitz](https://stackblitz.com/edit/stylifycss-solidjs-vite?file=src%2FApp.jsx)。

# 配置

上面的例子没有包括 Stylify 能做的所有事情:

*   定义[组件](https://stylifycss.com/docs/stylify/compiler#components)
*   添加[自定义选择器](https://stylifycss.com/docs/stylify/compiler#customselectors)
*   配置你自己的宏，比如`ml:20px`的左边距
*   定义[自定义屏幕](https://stylifycss.com/docs/stylify/compiler#screens)
*   您可以在模板中映射[嵌套文件](https://stylifycss.com/docs/bundler#files-content-option)
*   还有更多

请随意查看这些文档以了解更多信息💎。

# 让我知道你的想法！

我会很高兴得到任何反馈！Stylify 仍然是一个新的库，有很大的改进空间🙂。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***