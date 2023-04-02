# 开始使用 React & Google Firebase

> 原文：<https://javascript.plainenglish.io/use-a-firebase-db-inside-your-reactjs-project-2cfb56b51162?source=collection_archive---------9----------------------->

## 关于设置 React 项目和使用 Google Firebase 存储数据的教程。

![](img/38cabb79c78d77379a96e12fc58d544d.png)

Photo by Manoj shah from Pexels

[](https://firebase.google.com/) [## 重火力点

### 请于 2022 年 10 月 18 日亲自或在线参加我们的 Firebase 峰会。了解 Firebase 如何加强集成…

firebase.google.com](https://firebase.google.com/) [](https://reactjs.org/) [## react——用于构建用户界面的 JavaScript 库

### React 使得创建交互式 ui 变得不那么痛苦。为应用程序中的每个状态设计简单的视图，并反应…

reactjs.org](https://reactjs.org/) 

因此，您正在使用 React，并且想要一种快速简单的方法来存放您的数据。虽然有很多不同的方法来实现这一点，但我将向您展示的方法涉及 Firebase，这是一个免费的(在一定范围内)选项，快速且易于使用。

首先，您需要建立一个 React 项目。我写了一篇关于如何做到这一点的文章，可以在这里找到！

您还需要在您的计算机上安装 Node，所以确保通过运行命令`node -v`安装了它。如果没有安装，可以在这里下载[安装。](https://nodejs.org/en/download/)

一旦设置好 React 项目并安装了 NodeJS，就需要安装 Firebase。为此，请运行以下命令

```
npm install firebase
```

我们将希望实际进入 Firebase 并建立一个项目，在那里我们将存放我们的数据。要设置我们的项目，请访问[www.firebase.google.com](http://www.firebase.google.com)。点击主页上的**开始**按钮或右上角的**转到控制台**按钮。然后，您将使用您的 Google 帐户登录。

一旦创建了项目，就可以建立数据库了。对于这个例子，我将使用 Firestore 数据库，它允许我使用我所熟悉的 REST API。如果你不确定你应该使用哪一种，这里的[是不同类型及其优缺点的一个很好的分类。](https://blog.back4app.com/firebase-database/#What_are_the_Firebase_database_types)

要设置您的数据库，您需要点击左侧窗格并打开`build`菜单，在这里您会看到认证、应用检查、Firestore 数据库等选项。点击 Firestore database，它将向您展示创建一个集合以供使用的能力。[下面是 Firebase](https://firebase.google.com/docs/firestore/data-model) 中数据模型的分解。

接下来，我们将在应用程序中初始化 Firebase，并创建一个 Firebase 对象。为此，建立一个文件，并将其命名为`firebase.js`。出于演示的目的，我们将保持简单，从我们的数据库中抓取一些数据并将其放到页面上。

Our Firebase.js file

然后，为了实际使用我们的 Firebase 配置并访问我们的数据，我们将需要设置另一个文件来从数据库中获取数据并将其放在页面上:

Our React component for showing the title and body of our blog post

在上面的代码片段中，我们将 React 组件连接到我们的`firebase.js`文件。我们首先从数据库中获取我们的文章，映射数据并将其放到页面上。

创建完上面的两个文件后，你就可以开始开发了！

![](img/61985adaa884914340fbbec5ee418dd3.png)

虽然这是一个如何使用数据库中的数据的基本示例，但是您也可以将数据推送到数据库，以及编写一些复杂的逻辑来同时处理多个数据库。

我希望这篇文章是令人愉快的。如果你有任何反馈，发表评论，让我知道我可以改进的地方。如果你想看看我的其他帖子，可以在这里找到。我写的都是前端特有的东西，所以我有关于 Shopify 的[自定义主题开发的文章](/developing-custom-themes-for-shopify-getting-started-b137407c0cb7)、[基于类的 React 组件](/class-based-components-in-react-14335f0ee539)、 [Fetch API](https://avetwhocodes.com/fetching-data-from-an-api-with-the-fetch-api-in-react-5dbe0abcfb41) 、 [React](/level-up-your-react-skills-with-the-use-of-composition-766a41f544c9) 、 [TypeScript](https://jgrice01.medium.com/typescript-understanding-the-basics-a2264759cd2d) 、 [SASS](https://medium.com/codex/writing-better-sass-with-dynamic-class-generators-e486a0413d0d) 、[electronic](https://jgrice01.medium.com/want-to-build-desktop-apps-using-js-say-hello-to-electron-4f862c3b4e38)。感谢您的阅读，祝您愉快！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***