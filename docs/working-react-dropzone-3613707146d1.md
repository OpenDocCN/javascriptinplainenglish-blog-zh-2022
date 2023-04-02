# 如何使用 React Dropzone

> 原文：<https://javascript.plainenglish.io/working-react-dropzone-3613707146d1?source=collection_archive---------14----------------------->

## 创建上传目录组件

![](img/6d2900ab83c45505859f88bcc797a4dd.png)

Photo by [Tezos](https://unsplash.com/@tezos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在后台

我们在网站的自定义存储库部分遇到了一个问题。我们想要为整个存储库创建一个 JSON 树(将在本文后面解释问题陈述)。在今天的故事中，我们将讲述一个小而简单的问题及其解决方案。

## 问题陈述

我要解释的问题完全是我们在产品[定制回购](http://ihatereading.in/customrepo)中面临的问题。我们希望为其他开发人员开放自定义存储库部分，与更广泛的受众分享他们的架构和代码库，这样其他人也可以学习。但是为了提供方法，我们肯定需要输入来上传目录，而不是文件。

## 议程

以下几点将解释我们的目标和议程。我们努力实现的目标被清晰地表述为几点

*   我们需要上传目录，以便从中获取 JSON 树。
*   JSON 树是对象的集合。
*   每个对象都是上传目录的一个文件或文件夹，包含其详细信息，如内容、id、文件名和路径。
*   然后，我们可以将 JSON 存储在数据库中，并从中创建架构。
*   通过这种方式，用户可以在自定义回购部分上传架构。
*   这样，我们可以自动化创建和上传回购树的过程

## 入门指南

我们正在使用一个 npm 模块，该模块被广泛接受并用于处理目录或类似从本地系统上传文件到浏览器的功能。React dropzone 非常有用，被广泛接受，轻量级，易于使用的 npm 模块。当然，您可以自己创建一个输入上传组件，如果您从头开始学习 React，那么您应该尝试自己创建一个组件。

使用纱线或 npm 安装包装

```
yarn add react-dropzone
```

## 创建要上传的输入

我们需要一个输入或拖放区来拖放文件或上传我们想要上传的文件。我们可以简单地为此创建一个输入，并为它提供一些样式。

## 接受文件的方法

React dropzone 提供了钩子和几种方法来处理上传的文件。无论您定义什么方法和使用什么钩子，都要将它们作为文件上传输入的道具。这个过程非常简单，只需几行代码，您就可以创建上传组件。

仅使用 react-dropzone 提供的 Dropzone 挂钩。当文件被拖放时，这些钩子采取方法来处理文件，作为回报，它给我们一些道具，我们将这些道具传递给输入元素。

## 其他方法

对于 useDropzone 钩子中的每个输入，可以用其他方法来处理。输入元素可以访问和调用您将传递给钩子的任何方法。

## 翁德拉格

当用户拖放文件时调用的方法。

## 翁德罗普

一旦用户退出放置状态，该方法就需要采取某些操作。

## 证明文件

如果你想了解更多细节，这里有文档链接。

 [## 反应-下降区

### 编辑描述

react-dropzone.js.org](https://react-dropzone.js.org/) 

## 结论

这是 dropzone 入门的基础入门文章。如果您想阅读更多这样的故事，以开始使用这种有用的库和包，请访问我们的网站— [www.ihatereading.in](http://www.ihatereading.in)

下次见。祝大家愉快。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。***