# Node.js +带有 Docker 的数据库，用于本地开发

> 原文：<https://javascript.plainenglish.io/node-js-database-with-docker-for-local-development-285212c5162f?source=collection_archive---------3----------------------->

## 各种数据库的一站式解决方案。

![](img/ed3fd52dd4249d2f6376d0b4e133f357.png)

Photo by [fabio](https://unsplash.com/@fabioha?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/digital?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

今天我们将学习如何使用 Node.js 和任何数据库(Postgres/MySQL 等)创建一个成熟的后端应用程序。).

我们将使用 docker-compose 让应用服务器和数据库同时启动和运行，这可以改善我们开发体验。

我假设您已经了解了 docker 的基础知识，并且知道如何对一个基本的 Node.js 应用程序进行 docker 化。如果没有，可以看看下面这篇文章。

[](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) [## 像专业人士一样使用 Docker 和 NodeJS 项目！

### 在开发和生产中利用 Docker 的力量

levelup.gitconnected.com](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) 

## 在我们开始之前…

我用 ExpressJS 和 Typescript 创建了一个[专业样板。本文是这个系列的一部分。你可以在下面找到所有的文章。](https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate)

```
***** [**Creating a ExpressJS + Typescript Boilerplate**](/create-an-express-boilerplate-with-typescript-810eb6c29196) ***** [**How to setup Linter and Formatter for NodeJS**](/how-to-set-up-linter-formatter-for-node-js-d6b34c0c8be5) ***** [**How to handle multiple environments in NodeJS**](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) ***** [**Error Handling in NodeJS**](/error-handling-in-node-js-like-a-pro-ed210baa0600) ***** [**Request Validation in NodeJS**](https://medium.com/p/c69f2494cf18) ***** [**Using Docker Professionally with NodeJS**](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) ***** [**Using Docker for Local Development in NodeJS**](/node-js-database-with-docker-for-local-development-285212c5162f) ***** [**Logging in NodeJS**](/node-js-logging-for-professionals-6be07c003e7f) ***** [**Kubernetes with NodeJS**](https://levelup.gitconnected.com/kubernetes-deployment-with-nodejs-made-easy-eaeec32b62e3)
```

我们开始吧！

# 拿样板文件

首先，克隆 [express-docker 样板库](https://github.com/Mohammad-Faisal/express-typescript-docker)，其中我们有一个使用 TypeScript 的 express 应用程序和一个使用 docker-compose 的基本设置。

我们将在这个存储库之上集成数据库:

```
git clone [https://github.com/Mohammad-Faisal/express-typescript-docker.git](https://github.com/Mohammad-Faisal/express-typescript-docker.git)
```

# 但是为什么呢？

当您在本地开发时，每次使用`pgadmin`或`mysql`进入 PostgreSQL 服务器时，服务器可能会很无聊。

我们可以使用`**docker-compose**`的力量轻松集成数据库，确保团队中的所有人在开发时有相同的体验。

# 基础

打开 docker-compose.yml 文件，其中已经有一个名为`**express-typescript-docker**`的服务。我们将在此基础上为我们的数据库添加另一个服务。

我们还需要一个这两个服务共享的公共网络，因为我们的应用服务器需要与数据库服务器通信。

我们还需要一个用于数据库服务器的卷。所以我们总共需要三样东西。

*   数据库服务。
*   数据库将使用的一个 [docker 卷](https://docs.docker.com/storage/volumes/)。
*   共享的 [docker 网络](https://docs.docker.com/network/)。

# 定义数据库服务。

打开 docker-compose.yml 文件，在现有的`express-typescript-docker`服务下添加以下数据库服务

docker-compose.yaml

这里有几件事我们可以看看:

`**1\. environment**`:定义 MySQL root 密码。如果您不想使用 root 密码，可以创建一个新用户并分配一个密码。您甚至可以通过它创建一个新的数据库。

docker-compose.yaml

`**2\. volumes**`:我们在合成文件的末尾定义了一个卷，并将该卷附加到这个 docker 映像的`*/var/lib/mysql*`

因为 docker 映像的内存是短暂的，所以如果停止容器，会话之间的所有数据都将丢失，这是不希望的。

卷可以通过在会话之间保存数据来帮助我们避免这种情况。

`**3\. networks**`:这有助于我们像缝合针一样连接服务

并且，在 e `xpress-typescript-docker`服务上，添加一些新的依赖项

# 使用备用数据库

如果您想使用另一个数据库(如 PostgreSQL)，这是很容易做到的。你所要做的就是用下面的代码替换 MySQL 服务。

docker-compose.yaml

就是这样！有多简单？你对 MongoDB 感兴趣吗？我们也可以拥有它！

docker-compose.yaml

希望你现在明白 docker 在地方发展中的力量。无需安装，无需配置，没有特定于操作系统的难题！

# 更新服务器

我们需要修改服务器的配置，如下所示。

docker-compose.taml

depends_on 部分定义了我们应该等待数据库启动并运行，然后启动应用服务器。

# 测试一下

所以我们现在有了一个好的配置，但是如何测试呢？让我们先运行容器。

```
docker-compose up
```

这将正确地启动数据库和应用服务器。

# 使用 adminer 检查数据库。

让我们更好地利用 docker。有一个很好的应用叫做`adminer`，它是一个数据库工具，允许我们检查许多数据库。

让我们将它添加到 docker-compose.yml 文件中。在服务下，添加以下内容。

docker-compose.yaml

让我们再次运行 docker-compose 并转到`[**http://localhost:8080/**](http://localhost:8080/)`。您将看到一个登录页面。在此使用以下凭据登录数据库。

```
Server : mysql-docker
Username: root
Password: any_password
Database: test_db (optional)
```

您应该能够登录到该应用程序。

# 使用 Sequalize 连接到数据库。

好吧。所以我们现在可以连接到数据库。但是我们如何在内部连接数据库呢？我们将使用最流行的 ORM[Sequalize](https://sequelize.org/)来完成这项工作。先装吧。

```
yarn add sequelize mysql2yarn add -D @types/sequelize
```

要连接到数据库，您必须创建一个 Sequelize 实例。

让我们创建一个数据库 utils 文件，并在其中添加以下代码。

sequelize.ts

并更新 index.ts 文件以首先连接到数据库，然后启动服务器。

server.ts

现在，您只需运行下面的命令就可以让一切正常运行。

```
docker-compose up
```

并且看到下面的结果！

```
express-typescript-docker | Connection to database has been 
                            established successfully.express-typescript-docker | Server running successfully on port 3000
```

恭喜你！现在，您已经有了一个可以与数据库一起工作的 Node.js 应用程序，我们还有一个数据库监控工具作为奖励！

# 记住

不要忘记这种设置只适用于开发环境。对于生产，您可能希望将数据库与服务器分开。你可以使用专用的主机，或者从 AWS 这样的云服务中获得帮助。

# 解决纷争

如果您以前运行过容器，您可能会遇到一些密码问题。在这种情况下，您需要删除以前创建的卷。

```
docker volume prune
docker-compose down --volumes
```

# 清理:

Docker 会占用大量的磁盘空间。看到这一点

```
docker system df
```

您可以通过以下方式移除停止的容器、未使用的网络和悬挂图像

```
docker system prune
```

今天到此为止。祝你今天休息愉快！:D

```
**Want to Connect?**You can reach out to me via [**LinkedIN**](https://www.linkedin.com/in/56faisal/) or my [**Personal Website**](https://www.mohammadfaisal.dev/blog)
```

# 资源

*   [Docker 网络文档](https://docs.docker.com/network/)
*   [Docker 卷文档](https://docs.docker.com/storage/volumes/)

## Github 回购

[](https://github.com/Mohammad-Faisal/express-sequelize-docker-compose) [## GitHub-Mohammad-fais al/express-sequelize-docker-compose

### 点击此处获取全文 https://www . Mohammad fais al . dev/blog/express-database-docker-compose 今天我们将学习如何…

github.com](https://github.com/Mohammad-Faisal/express-sequelize-docker-compose) 

## 更多 NodeJS 文章:

[](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) [## 像专业人士一样使用 Docker 和 NodeJS 项目！

### 在开发和生产中利用 Docker 的力量

levelup.gitconnected.com](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) [](/node-js-logging-for-professionals-6be07c003e7f) [## 专业人员的 Node.js 日志记录

### 发挥温斯顿和摩根的全部潜力

javascript.plainenglish.io](/node-js-logging-for-professionals-6be07c003e7f) [](/error-handling-in-node-js-like-a-pro-ed210baa0600) [## 像专家一样处理 Node.js 中的错误

### 你需要知道的一切。

javascript.plainenglish.io](/error-handling-in-node-js-like-a-pro-ed210baa0600) [](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) [## 如何在 NodeJS 中处理多种环境

### 如何建立一个专业的节点工程

blog.devgenius.io](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*