# 资产和创建-反应-应用程序:处理它们的正确方法是什么？

> 原文：<https://javascript.plainenglish.io/assets-and-create-react-app-whats-the-right-way-to-handle-them-a145587bd506?source=collection_archive---------1----------------------->

![](img/f5eab98fd1322f58a27d97c3bfaa4e46.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

通常，网页的公共文件夹是存放图像、视频和 CSS 文件等资产的地方。但是，如果应用程序是用 create-react-app 创建的，那么这里就不是推荐调用它们的地方。要了解这里发生了什么，必须查看 create-react-app 中的一个模块。

create-react-app 使用了令人眼花缭乱的软件包。一个这样的项目是网络包。它是一个“*静态模块捆绑器*”，检查一个 JavaScript 应用程序并构建它所谓的“*依赖图*”。本质上，它找到文件之间的任何依赖关系，收集所有必要的模块，并将它们放在尽可能少的包中，以便浏览器加载。

为了利用 webpack 提供的优势，建议导入 JavaScript 文件中的资源，而不是将它们添加到 public 文件夹中。在运行 create-react-app 之后，您可能已经注意到有一个样式表和一个图像文件被导入到`App.js`中。两者都位于`src`目录中，而不是 public 文件夹中。

这是因为 webpack 不处理公共文件夹中的文件。相反，它被设计为找到所有的依赖项，并为了效率将它们捆绑在一起。例如，如果有人希望分离样式问题，并为每个组件创建一个样式表，那么 webpack 会将导入的 CSS 文件捆绑在一起，从而最大限度地减少网络请求的总量。另一个好处是，任何丢失或相对路径错误的导入文件都会为用户抛出一个编译错误，而不是 404 错误。

使用 create-react-app 可以快速创建新的 react 应用程序，因此了解幕后发生的事情非常重要。应用程序依赖于大量的资产，如样式表、图像和字体。Webpack 将识别这些依赖性，并最小化它们以实现更快的构建时间。请记住将它们放在公共文件夹之外的某个地方！

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*