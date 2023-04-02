# 逐步了解 Webpack 的 5 个优化技巧

> 原文：<https://javascript.plainenglish.io/learn-5-optimization-tips-for-webpack-step-by-step-cc81eb41a1c7?source=collection_archive---------5----------------------->

![](img/25a1c4c51b39f435573625736d888d7f.png)

Photo by [Green Chameleon](https://unsplash.com/@craftedbygc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**这次，让我们来看看 webpack 的 5 种优化技术。大家一起讨论一下，看看有没有更多更好的！**

## **1。首先，让我们了解一下缓存加载器**

那么，在什么场景下我们可以使用缓存加载器进行优化呢？对，没错，为了多次构建项目，为了加快后续的构建，可以使用 cache-loader 来启用缓存的加载器。

好吧，我们一步一步来讨论。

第一步:安装:

```
**npm i cache-loader -D**
```

第二步:配置:

```
**{****test: /.js$/,****use: [****'cache-loader',****'thread-loader',****'babel-loader'****],****}**
```

优化缓存加载器的速度是否更简单？

## **2。让我们来看看排除&包含**的优化

对于我们开发工程师来说，在项目中，有一些文件是不需要打包的。您可以在配置期间指定某些文件不参与构造，以防止 webpack 检索它，从而提高编译效率。当然，你也可以指定一些文件需要编译。这是你可以使用`exclude`和`include`的时候。

让我们直接解释如何配置它:

```
**{****test: /.js$/,****include: path.resolve(__dirname, '../src'),****exclude: /node_modules/,****use: [****'babel-loader'****]****}**
```

`exclude`:对于不需要编译的文件；

`include`:针对需要编译的文件。

## **3。让我们看看压缩 CSS 代码的魔力**

简单来说，css-minimizer-webpack-plugin 是用来对 css 代码进行压缩和去重的，我们来看看具体的步骤。

第一步:安装:

```
**npm i css-minimizer-webpack-plugin -D**
```

第二步:配置:

```
**const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');****optimization: {****minimizer: [****new CssMinimizerPlugin(),****],****}**
```

## **4。解释完 CSS 的压缩，我们来压缩一下 JS 代码的使用**

一看到 JavaScript，我们应该马上想到 terser-webpack-plugin。是的，我们来看看。

第一步:安装:

```
**npm i terser-webpack-plugin -D**
```

第二步:配置:

```
**const TerserPlugin = require('terser-webpack-plugin');****optimization: {****minimizer: [****new CssMinimizerPlugin(),         new TerserPlugin({****terserOptions: {****compress: {****drop_console: true,                 },****},****}),****],****}**
```

## **5。最后一个，我们来看看束分析器**

使用 webpack-bundle-analyzer 查看打包的 bundle 文件的体积，以便有针对性地进行相应的体积优化。这个的使用也是最常见的。

第一步:安装:

```
**npm i webpack-bundle-analyzer -D**
```

第二步:配置:

```
**const {BundleAnalyzerPlugin} = require('webpack-bundle-analyzer');****plugins: [****new BundleAnalyzerPlugin(),****]**
```

**感谢您的阅读，期待您的关注，让我们共同进步。**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***