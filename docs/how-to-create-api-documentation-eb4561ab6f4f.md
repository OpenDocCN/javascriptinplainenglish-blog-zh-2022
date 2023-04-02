# 如何创建 API 文档

> 原文：<https://javascript.plainenglish.io/how-to-create-api-documentation-eb4561ab6f4f?source=collection_archive---------17----------------------->

## **第 2 部分:建立您的第一个 API 文档**

![](img/fc2e2d770a1e499894e92103ef170c3a.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

本文是本系列文章的第二部分。如果你错过了上一篇文章，你可以在下面找到它。我们还研究了各种可用的 API 规范。

[](/how-to-create-api-documentation-83941174e6b2) [## 如何创建 API 文档

### 第 1 部分:创建您的第一个 API 文档

javascript.plainenglish.io](/how-to-create-api-documentation-83941174e6b2) 

在这里，我们将卷起袖子，开始记录一个真正的 API。为此，我们将利用 OpenAPI 规范，因为它是最常用的规范。OpenAPI 也有很多围绕它的工具，这些工具上有惊人的资源，可以让你快速上手。

## **我们的 API 工具**

我们将利用一个包管理器，它将允许我们指定 API 的结构。这将包括数据模式、端点描述、参数描述、定义、安全性、主体/查询参数、响应、状态代码和请求结构。

这个工具利用了一个隐藏的 swagger 规范来处理所有这些。这个包将为我们生成一个包含所有 API 文档信息的 ***swager.json*** 文件。自动生成的文件将遵循 swagger 格式和规范。

***注意:*** 这是一个 JavaScript 包，我们将记录一个基于 NodeJs 的应用程序。

## **安装和设置**

使用创建快速脚手架项目。

初始化新的应用程序。

```
$ npm inint -y
```

安装 express

```
$ npm install express –save
```

在目录中，创建一个文件夹，并将其命名为 src。在 src 文件夹中，创建两个文件，即 app.js 和 server.js。

## **app.js**

App.js 将是我们的应用入口。Server.js 将运行我们的应用程序开发服务器。

**server.js**

现在我们已经用 swagger 配置了 API 文档。在下一部分中，我们将研究如何在处理请求和响应的控制器或路由上添加各种注释。

如果您想记录一个现有的项目，请继续安装它。

```
$ npm install — save-dev swagger-autogen
```

在应用程序的根目录下，创建一个名为 ***swagger.js*** 的文件，并添加以下代码。

**配置 swagger.js**

这应该是我们的 API 自动生成的根条目文件。这里我们将为***swagger-autogen***指定文件，以查找我们的注释并生成它们。
为了确保***swagger-autogen***找到并记录我们的 API，我们将为其提供注释。

这些注释将具有与各种端点、请求结构和响应相关的各种描述。您需要将这些注释放在处理 API 请求的函数中。注释可以放在控制器函数内部。

现在，我们可以使用 swagger 注释来注释掉各种 API。注释应该包含在处理控制器和路由请求的函数中。

Swagger-autogen 将在运行时生成我们的 API，并将其格式化为 OpenAPI 规范。

## **出发前**

在下一篇文章中，我们将对路线和控制器添加必要的注释。我们还将深入研究如何处理必要的查询和主体参数，以便自动生成 swagger OpenAPI。

每周三，我都会发送一封独家邮件，里面有我发现的有用的、与技术写作相关的技巧、文章、应用、书籍和想法。

[***加入像你一样想提高技术写作水平的人吧。***](https://artisanal-thinker-2556.ck.page/6e2ba71172)

## **更多阅读内容**

[](/how-to-create-api-documentation-83941174e6b2) [## 如何创建 API 文档

### 第 1 部分:创建您的第一个 API 文档

javascript.plainenglish.io](/how-to-create-api-documentation-83941174e6b2) [](/how-to-effectively-collaborate-with-git-github-as-a-software-developer-f3e073b46ed5) [## 作为软件开发人员，如何有效地与 Git/GitHub 协作

### 有效协作的 Git/GitHub 清单

javascript.plainenglish.io](/how-to-effectively-collaborate-with-git-github-as-a-software-developer-f3e073b46ed5) 

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***

## 进一步阅读

[](https://plainenglish.io/blog/5-dev-tools-for-documenting-react-code-like-a-pro) [## 像专家一样记录 React 代码的 5 个开发工具

### React 作为构建复杂前端应用程序的库非常有用，但它也需要大量的工具…

简明英语. io](https://plainenglish.io/blog/5-dev-tools-for-documenting-react-code-like-a-pro) [](/bad-documentation-is-tech-debt-heres-how-you-solve-it-ce1d0b3ee760) [## 糟糕的文档是技术债务——以下是解决方法

### 如果你想快速行动，尽可能少破坏东西，文档文化是至关重要的，那么为什么好的文档…

javascript.plainenglish.io](/bad-documentation-is-tech-debt-heres-how-you-solve-it-ce1d0b3ee760)