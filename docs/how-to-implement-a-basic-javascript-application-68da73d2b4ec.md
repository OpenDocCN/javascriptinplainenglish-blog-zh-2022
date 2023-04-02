# 如何实现一个基本的 JavaScript 应用程序

> 原文：<https://javascript.plainenglish.io/how-to-implement-a-basic-javascript-application-68da73d2b4ec?source=collection_archive---------9----------------------->

## 关于实现基本 JavaScript 应用程序的教程。

![](img/677544d3a711c362730266299e69bae3.png)

Illustration by the author

在本系列的前一篇文章[中，我们学习了在开始编写应用程序之前从其他人那里获取输入。在我们澄清了项目涉众的所有疑问之后，我们就可以将我们的](https://how-to.dev/how-to-collect-inputs-for-your-project)[原型](https://github.com/how-to-js/hello-world/tree/prototype)转化为 JavaScript 应用程序了。

# 我们在做什么？

本系列的目标是用最简单的用例展示现代前端 JavaScript 应用程序的所有方面:

![](img/7993109a823746988f5ea457f8349918.png)

# 内联 JavaScript

第一步，我们需要用 JavaScript 完成我们的纯 HTML 原型的一些部分。最简单的方法是使用内联 JS。所以，我们的`index.html`就变成了:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Hello World!</title>
  </head>
  <body>
    <script type="text/javascript">
      const element = document.createElement("h1");

      element.innerText = "Hello World!";

      document.body.appendChild(element);
    </script>
  </body>
</html>
```

如果您对这里发生的事情以及它如何产生与以前相同的页面感兴趣，您可以在这里阅读更多关于 DOM 操作的。

# 加载 JS 文件

将所有代码都放在`index.html`文件中是不可伸缩的——这将很快变得不方便。相反，让我们将代码分成单独的 HTML 和 JS 文件:

`script.js`:

```
const element = document.createElement("h1");

element.innerText = "Hello World!";

document.body.appendChild(element);
```

并更新`index.html`:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Hello World!</title>
  </head>
  <body>
    <script type="text/javascript" src="./script.js"></script>
  </body>
</html>
```

这样好多了！

# JavaScript 模块

在上一步中，我们以传统的方式包含了 JavaScript 一次一个文件。现代 JS 允许我们在模块中编写代码，这些模块定义了它们内部的依赖关系，浏览器解析路径并加载必要的文件。截至目前，市面上几乎 95%的浏览器都已经有这个功能了([来源](https://caniuse.com/es6-module-dynamic-import))。

让我们在应用程序中使用它！

首先，我们将消息移动到一个单独的文件，`greeting.js`:

```
export const greetingMessage = "Hello World!";
```

注意我们在`const greetingMessage...`前用`export`。这让 JS 知道这个常量应该可以从其他文件导入。

现在，我们可以在项目中任何需要的地方轻松地导入这个值。我们将对更新后的`script.js`做同样的事情:

```
import { greetingMessage } from "./greeting.js";

const element = document.createElement("h1");

element.innerText = greetingMessage;

document.body.appendChild(element);
```

最不需要的更新是在`index.html`的导入中更改`type`属性:

```
<title>Hello World!</title>
   </head>
   <body>
-    <script type="text/javascript" src="./script.js"></script>
+    <script type="module" src="./script.js"></script>
   </body>
 </html>
```

你可以在本文中阅读更多关于本地 ES 模块的内容。

# 把它变成一个 npm 包

npm 是一个包管理器，它允许我们轻松地下载社区包以在我们的应用程序中使用。它最初是为节点、服务器端 JavaScript 开发的，但是几年前，它已经成为前端 JavaScript 的标准。在我们的例子中，它将允许构建脚本和构建依赖项的简单配置。

要初始化这个包，您可以在您的包文件夹中运行`npm init`:

```
$ npm init
This utility will walk you through creating a `package.json` file.
It covers only the most common items, and it tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (hello-world)
version: (1.0.0)
…
```

npm 提供了合理的默认值，因此在大多数情况下，您应该可以选择建议的值。成功运行该命令后，您将在文件夹中创建`package.json`。

# 网络包

使用原生 ES 模块可以在大多数浏览器中工作，但是在现实世界的项目中，您仍然会看到 JS 作为构建过程的一部分被捆绑在一起。为什么？在项目中，您通常想做很多事情:

*   编译 TypeScript 或任何其他能编译成 JavaScript 的语言。
*   减少交付给用户的文件数量。
*   同时，对我们将代码分成的块的大小有很好的控制。
*   包括一些缓存破坏技术——比如将文件的缓存添加到它的名字中。

我在这里进一步讨论原因。

JavaScript 最流行的 JS bundler 是 Webpack。让我们将它添加到我们的项目中！首先，我们需要安装它:

```
$ npm install webpack --save-dev

added 77 packages, and audited 78 packages in 7s

9 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

如果成功，这个命令将下载 webpack 文件，并将它们添加到`package.json`中的开发依赖项中。

# Git 忽略

如果您使用 git——正如您应该做的那样——将这个值设置为`.gitingore`:

```
node_modules
dist
```

它会将两个文件夹都保留在存储库之外:

*   `node_modeles`-存储所有第三方依赖项的地方。它通常很大，可以是特定于操作系统的，每个环境都应该直接从 npm 存储库中获取包
*   `dist`-会不断更新，需要时可以从源代码重新构建

# 建设

要开始使用 webpack，在同一个`package.json`文件中，让我们将`build`添加到我们的`scripts`部分:

```
{
  …
  "scripts": {
    "build": "webpack --mode production",
    …
  },
```

`--mode production`明确设置 Webpack 构建代码的方式，这样我们就可以避免在控制台中看到以下警告:

```
WARNING in configuration
The 'mode' option has not been set, webpack will fall back to 'production' for this value.
Set 'mode' option to 'development' or 'production' to enable defaults for each environment.
You can also set it to 'none' to disable any default behavior. Learn more: https://webpack.js.org/configuration/mode/
```

我们用`npm run build`运行构建。第一次运行将安装一些附加的依赖项:

```
$ npm run build

> hello-world@1.0.0 build
> webpack

CLI for webpack must be installed.
  webpack-cli (https://github.com/webpack/webpack-cli)

We will use "npm" to install the CLI via "npm install -D webpack-cli".
Do you want to install 'webpack-cli' (yes/no): yes
```

第一次构建将会失败，因为默认的 webpack 配置会在`./src`文件夹中查找代码。我们可以通过以下方式修复它:

*   将`script.js`重命名为`index.js`，
*   将`index.js`和`greeting.js`都移动到新文件夹`./src`

为了使用我们构建的代码，让我们用下面的变化来更新`index.html`:

```
<title>Hello World!</title>
   </head>
   <body>
-    <script type="module" src="./script.js"></script>
+    <script src="./dist/main.js"></script>
   </body>
 </html>
```

你可以在这里找到我现阶段的代码[。](https://github.com/how-to-js/hello-world/tree/webpack-build)

# 生成`index.html`

一些 JS 捆绑器使用索引文件作为配置来确定应该构建什么文件。在 Webpack 中，通常是反过来的:配置文件负责定义应该如何生成索引文件。一开始可能有点混乱，但是当我们在下一步中到达开发服务器时，它工作得很好。那我们就在这里设置吧！

## 添加`webpack.config.js`

首先，我们添加配置文件`webpack.config.js`:

```
module.exports = {
  mode: "production",
};
```

这一改变让我们简化了`package.json`中的构建脚本:

```
"scripts": {
-    "build": "webpack --mode production",
+    "build": "webpack",
     "test": "echo \"Error: no test specified\" && exit 1"
   },
```

因为模式已经在配置中设置好了。在这个阶段，构建应该像以前一样工作。

[示例代码](https://github.com/how-to-js/hello-world/tree/webpack-config)。

## 添加`html-webpack-plugin`

接下来，我们需要添加另一个开发依赖项:

```
$ npm install --save-dev html-webpack-plugin
```

要使用它，我们需要将`webpack.config.js`更新为:

```
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "production",
  plugins: [new HtmlWebpackPlugin({ title: "Hello World!" })],
};
```

现在，拆下旧的`index.html`。

最终构建产生两个文件:

```
$ npm run build

> hello-world@1.0.0 build
> webpack

asset index.html 215 bytes [emitted]
asset main.js 116 bytes [compared for emit] [minimized] (name: main)
orphan modules 47 bytes [orphan] 1 module
./src/index.js + 1 modules 218 bytes [built] [code generated]
webpack 5.74.0 compiled successfully in 157 ms
```

其输出可以在`dist`文件夹中找到:

```
$ ls dist
index.html      main.js
```

看一下[代码来对比](https://github.com/how-to-js/hello-world/tree/generate-index)。

# 开发服务器

为了帮助开发，Webpack 提供了一个开发服务器。

我们为什么要烦恼呢？开发服务器:

*   监视文件更改
*   每次有变化时都要重建
*   在浏览器中重新加载应用程序

每次你修改代码时，它很容易为你节省几秒钟的时间，在你的工作日里，你可能要修改几百次。

很容易配置:只需将`start`脚本添加到`package.json`中:

```
"main": "src/index.js",
   "scripts": {
     "build": "webpack",
+    "start": "webpack serve",
     "test": "echo \"Error: no test specified\" && exit 1"
   },
```

第一次运行该命令时，Webpack 会建议安装必要的依赖项- `webpack-dev-server`:

```
$ npm run start

> hello-world@1.0.0 start
> webpack serve

[webpack-cli] For using the 'serve' command you need to install: 'webpack-dev-server' package.
[webpack-cli] Would you like to install the 'webpack-dev-server' package? (That will run 'npm install -D webpack-dev-server') (Y/n) Y
```

让我们来看看它的实际应用:

```
$ npm run start

> hello-world@1.0.0 start
> webpack serve

<i> [webpack-dev-server] Project is running at:
<i> [webpack-dev-server] Loopback: http://localhost:8080/
…
```

当你在你的机器上启动它的时候，你可以访问这个 URL 并测试它是否真的在你保存到你的文件中的任何改变后重新加载。

查看[参考代码](https://github.com/how-to-js/hello-world/tree/dev-server)。

# 想了解更多关于 webpack 的信息吗？

我在 Udemy 上有一门关于 [webpack 的课程。你会发现一个类似的，一步一步的方法。](https://bit.ly/WebpackCourse)

我希望技术上的转变没有把你吓跑，你仍然在继续你的项目！在评论中分享你的进步或挣扎。

*最初发布于*[*https://how-to . dev*](https://how-to.dev/how-to-implement-a-basic-javascript-application)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***