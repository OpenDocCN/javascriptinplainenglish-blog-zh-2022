# 如何用 Node.js 建立到 MongoDB 的连接

> 原文：<https://javascript.plainenglish.io/how-to-establish-a-connection-to-mongodb-with-node-js-8685f31bff2c?source=collection_archive---------10----------------------->

## MongoDB

## 如何用 Mongoose 创建到 MongoDB 的连接？

![](img/ada1f458d8187a563ceb9b60c8b5cf6e.png)

mongodb.com

MongoDB 是一个数据库集合平台，其中保存了预定义的数据，这些数据具有可以用编程语言访问的模式。今天，我们将看看如何使用 Node.js 连接到数据库。

如果您在 MongoDB 上还没有帐户，请创建一个，这是数据库管理所必需的，[这里是](https://www.mongodb.com/)。

## 创建一个组织

现在，我们可以专注于 MongoDB 提供的服务，从现在开始，我们将致力于他们的云页面[这里](https://cloud.mongodb.com/v2)。

首先，我们需要创建一个组织，在一个地方用一个名字存储我们所有的集群。你可以把一个组织想象成你的团队，它拥有你的团队需要瞄准的所有项目。

![](img/908a799a73cf03fb1aad977a34477ab0.png)

在主云页面上，您可以创建自己的组织，然后邀请团队成员。现在您可以输入您的组织名称并选择 MongoDB Atlas。

## 项目创建

网站将要求您创建一个项目并填写相关信息。创建项目后，您可以通过点击`Build a Database`按钮来构建您的第一个数据库。

![](img/e4e59077bd4a831259f1dad3569ec7d1.png)

## 集群创建

在此步骤中，请选择您希望如何部署数据库。您可以从`serverless`(0.10 美元/1M 读数)、`dedicated`(0.80 美元/小时)或`shared`(免费)中进行选择，我们将在这里使用这些选项。

![](img/53720c9b69f77cad513a0fe79f52c5b9.png)

现在选择您想要使用的云提供商，您可以从`AWS`、`Google Cloud`或`Azure`中选择。

接下来，选择一个您希望运行数据库的服务器的大致位置。运行这两个接下来的设置，如果你想调整它们，但预定义的设置应该没问题。

最后，为集群选择一个名称。

![](img/e56966011ea6e86756646d87d8e93f4b.png)

在最后一步中，您将创建授权凭证，通过它您可以操作数据库数据(名称和密码)。

然后，选择您希望授予哪些 IP 地址来操作数据库的数据。如果您想允许从任何地方进行修改访问，请输入 IP 地址`0.0.0.0`。

## 初始化 Node.js 项目

我们可以像往常一样启动一个项目的存储库——通过键入命令`npm init`,然后我们可以继续填写关于该项目的信息。我们需要安装两个 NPM 软件包— `mongoose`和`dotenv`。

包`mongoose`用于以更简单的方式访问 MongoDB 数据库，包`dotenv`用于存储后端敏感数据，这些数据不应该被前端用户看到。

## 连接到数据库

在我们创建了 Node.js 项目和我们需要的一切之后，我们可以将我们的应用程序连接到它。在部署页面上，单击我们刚刚创建的集群上的`Connect`按钮。

现在，我们可以选择`Connect your application`选项。Node.js 的版本可以在 modal 的顶部输入(如果您想用不同的编程语言连接也可以)。将显示一个连接字符串，您可以使用它通过您的应用程序进行连接。

![](img/690eb73d1be949fa23924851bd7dcdb9.png)

在将字符串插入应用程序之前，我们需要用之前设置的凭证之一替换登录凭证。全权证书的格式为`username:password`。

现在，我们可以将连接字符串粘贴到我们的`.env`文件中，并使用适合该值的输入键:

```
**MONGODB**=mongodb+srv://**admin**:**admin**@cluster0.bn1ofkw.mongodb.net/?retryWrites=true&w=majority
```

现在，我们可以导入 2 个 NPM 包，并从主 JavaScript 文件的`.env`文件中提取`MONGODB`变量，如下所示:

```
const **mongoose** = require(’mongoose’);
require(’dotenv’).**config**();const { **MONGODB** } = process.env;
```

导入所有必需的包和变量后，我们可以在主 JavaScript 文件中建立连接，如下所示:

```
mongoose.**connect**(
    **MONGODB**,
    { useNewUrlParser: true, useUnifiedTopology: true },  
    () => console.**log**(’Successfully connected to database.’)
);
```

建立连接后，我们的控制台会显示一条消息，提示成功，一切就绪。

## **结论**

数据库可能是项目中非常有用的工具，选择 MongoDB 平台是一个很好的开始。我希望这篇文章能帮助您澄清 MongoDB 系统，如果您在下一个项目中开始使用这项技术，我会很高兴。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*