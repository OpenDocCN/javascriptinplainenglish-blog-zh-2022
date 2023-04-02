# 像专家一样为你的 JavaScript 项目创建一个配置文件

> 原文：<https://javascript.plainenglish.io/create-a-config-file-for-your-javascript-project-like-a-pro-42d098a43179?source=collection_archive---------5----------------------->

## 为什么我们需要一个配置文件，如何创建它？

![](img/bb36e1c69139116d0caa0604f91dc600.png)

Photo by [Surface](https://unsplash.com/@surface?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/files?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

现代的 JavaScript 框架需要配置文件。配置文件配置文件的简称包含项目开始时需要的初始参数和设置的列表。

它可以是任何东西，比如不同开发环境、语言设置、用户设置等中数据库 URL 的连接字符串。

但是，如果是私有或敏感的信息，比如 API 密钥或登录凭证，建议将信息放在。而不是在配置文件中。

有人可能会说，我们可以将所有东西放入不同的变量中，并按预期运行应用程序，但正如我上面所说的，开发人员应该尝试编写干净且良好的可伸缩代码。

开发应用程序时，编写他人能够理解的简洁代码总是明智的。配置文件可以帮助你做到这一点。

有三种不同的方式来编写你的配置文件*。它们如下-*

1.  JSON
2.  YAML
3.  初始化设置文件的后缀名

在开发 Javascript 应用程序时，开发人员更喜欢以 JSON 格式编写配置文件。

让我们用 MongoDB 数据库为用 node 编写的服务器应用程序创建一个简单的配置文件。

通过键入以下命令，启动一个新的节点应用程序并下载所有依赖项-

```
npm init
npm i --save express
```

在项目的根目录下创建一个 config.js 文件。将以下代码添加到其中:

```
const config = {
 app: {
   port: 3000, 
   name: 'myapp'
 },
 db: {
   host: 'localhost',
   port: 27017,
   name: 'db'
 }
};module.exports = config;
```

在项目的根目录下创建一个 db.js 文件。将以下代码添加到其中:

```
const mongoose = require('mongoose');
const config = require('./config');const { db: { host, port, name } } = config;
const connectionString = `mongodb://${host}:${port}/${name}`;
mongoose.connect(connectionString);
```

现在，将以下代码添加到 app.js 文件中:

```
// app.js
const express = require('express');
const config = require('./config');const app = express();
app.listen(config.app.port);
console.log(config.app.name);
```

以上代码是为节点项目创建配置文件的最简单方法。现在，您可以通过向文件添加更多信息来增加复杂性，并根据您的用例来使用它。

上面的代码更容易阅读，所有的配置信息都保存在一个文件中。

您也可以从 npm 安装配置包，并通过阅读文档获得相同的结果，但是如果您愿意，现在可以忽略它。

感谢您阅读帖子。我希望你喜欢它。

**你在应用程序中使用配置文件吗？**

在任何开源项目中，您是否见过类似但稍微复杂一点的配置文件？或者

你是否不愿意使用它，因为你可能已经发现了实现相同结果的不同方法？

请在评论区告诉我。我很想知道你的意见。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*