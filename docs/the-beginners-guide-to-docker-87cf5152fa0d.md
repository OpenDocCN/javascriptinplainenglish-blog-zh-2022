# 码头工人入门指南

> 原文：<https://javascript.plainenglish.io/the-beginners-guide-to-docker-87cf5152fa0d?source=collection_archive---------10----------------------->

## 软件工程

## 包含 6 个最常用命令的示例

![](img/25e30a7488ea576d832d24129660f611.png)

Photo by [Venti Views](https://unsplash.com/@ventiviews?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/docker?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你好。

在这篇文章中，我将讨论 Docker，它是什么，你如何创建一个简单的容器，以及一些你日常生活中最常用的命令。如果你已经熟悉 Docker，希望你能学到一些新东西；如果你只是刚刚开始，你会得到一份享受。

因此，不再拖延，让我们直接进入主题。

# 介绍

Docker 是一个工具，它允许您以容器化的格式轻松部署您的应用程序。这意味着应用程序及其所有依赖项和库可以打包到一个容器中，该容器可以在任何安装了 Docker 的机器上运行。

是的，“嗯，它在我的机器上工作”不再是一个有效的借口！

在 Docker 中，容器是一个轻量级的、独立的、可执行的包，它包含了运行应用程序所需的一切，包括代码、运行时、库、环境变量和任何其他依赖项。

## 图像和容器？那些是什么！

容器相互隔离，并与主机系统隔离，因此它们可以在任何环境和任何主机上运行，不会发生冲突或干扰。

它们是从 Docker 映像创建的，Docker 映像是包含创建容器所需的所有指令和依赖项的模板文件。您可以将 Docker 映像视为容器的蓝图，将容器视为该蓝图的运行中的*实例*。这允许你调出同一个蓝图的多个*实例*。

这使得容器非常有用，因为它们允许您以一致和可移植的方式打包和分发应用程序。

您可以在自己的机器上开发和测试您的应用程序，然后轻松地将它们部署到任何其他安装了 Docker 的机器上，这样就可以轻松地扩展和管理您的应用程序，并确保它们在任何环境下都能以相同的方式运行。

# 入门指南

以下是开始使用 Docker 的基本步骤:

1.  在你的机器上安装 Docker。Docker 可用于 Windows、Mac 和 Linux，因此您可以在各种系统上安装它。
2.  一旦安装了 Docker，您就可以开始使用容器了。
3.  要创建 Docker 容器，您需要一个 Docker 文件。这是一个简单的文本文件，包含构建容器的说明，例如使用哪个基础映像、安装哪些依赖项以及如何配置容器。在下一节中，我们将通过示例看到这一点！
4.  一旦有了 Docker 文件，就可以使用`docker build`命令构建 Docker 映像。这将读取 docker 文件中的指令，并创建一个可以用来创建一个或多个容器的图像。
5.  要运行 Docker 容器，可以使用`docker run`命令。这将启动容器并在其中运行应用程序。您还可以分别使用`docker stop`和`docker start`命令来停止和启动容器。
6.  要与他人分享您的 Docker 图像，您可以将其推送到 Docker Hub 等注册表中。这将允许其他人轻松获取您的映像并在他们自己的系统上运行。

## 创建 Dockerfile 文件

下面是一个简单的 Docker 文件示例，可用于构建 Docker 映像:

**注意:***docker file 通常放在项目的根目录下。*

```
FROM node:latest

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

COPY package.json /usr/src/app

RUN npm install

COPY . /usr/src/app

EXPOSE 3000

CMD ["npm", "start"]
```

让我们来看看这有什么作用:

*   这个 Dockerfile 文件使用 Node.js 基础映像的最新版本
*   在`/usr/src/app`创建一个目录
*   并将它设置为工作目录
*   然后它将`package.json`文件复制到我们创建的目录中
*   使用`npm`安装依赖项
*   将应用程序代码的其余部分复制到容器中
*   容器暴露端口 3000
*   当容器启动时，运行`npm start`命令，启动应用程序。

要了解关于 docker 文件的更多信息以及您可以用它做什么，您可以参考以下文档:

[](https://docs.docker.com/engine/reference/builder/) [## Dockerfile 文件参考

### Dockerfile 文件的格式如下:指令不区分大小写。然而，惯例是让他们…

docs.docker.com](https://docs.docker.com/engine/reference/builder/) 

## 建立码头工人形象

要使用这个 Docker 文件构建 Docker 映像，可以运行以下命令:

```
docker build -t my-node-app .
```

这将基于 Docker 文件中的指令创建一个名为`my-node-app`的 Docker 映像。

## 运行 Docker 容器

然后，您可以使用这个映像通过以下命令运行 Docker 容器:

```
docker run -p 3000:3000 my-node-app
```

这将启动一个基于`my-node-app`映像的 Docker 容器，将主机上的端口 3000 映射到容器中的端口 3000，并在容器内部运行`npm start`命令。

# Docker 命令

以下是一些最常用的 Docker 命令:

**注意:** *有关以下任何命令的更多信息，您可以使用 Docker 文档或运行* `**docker <command> --help**` *命令来查看选项的完整列表。*

## 码头工人建造

此命令用于从 Docker 文件构建 Docker 映像。

要使用`docker build`命令，您需要指定包含 Dockerfile 的目录的路径，以及您想要创建的图像的名称和可选标签。

例如，以下命令将使用当前目录中的 docker 文件构建一个名为`my-image`的映像:

```
docker build -t my-image .
```

`-t`标志指定图像的名称和可选标签，末尾的`.`指定包含 docker 文件的目录的路径。

`docker build`命令有许多其他选项和参数，可以用来定制构建过程。

## 码头运行

该命令用于基于 Docker 映像运行 Docker 容器。

要使用`docker run`命令，您需要告诉它想要用来创建容器的 Docker 图像的名称或 ID。

例如，以下命令将基于`my-image`图像创建一个 Docker 容器:

```
docker run my-image
```

默认情况下，`docker run`命令会创建一个新的容器并立即启动它。您还可以使用它来*启动*之前已经*停止*的容器。

`docker run`命令有许多其他选项和参数，可以用来定制容器。您还可以使用`-e`标志在容器中设置环境变量，或者使用`-v`标志从主机挂载一个卷。

## 码头停车

该命令用于停止一个或多个正在运行的 Docker 容器。

当您运行这个命令时，Docker 向容器内部的主进程发送一个信号，指示该进程正常关闭。如果进程没有在指定的时间内关闭(默认为 10 秒)，Docker 会发送另一个信号，强制终止进程。

要使用此命令，您需要提供一个或多个容器 id 或名称。例如，如果您想要停止一个名为`my-container`的容器，您可以运行以下命令:

```
docker stop my-container
```

要停止多个容器，可以使用如下命令:

```
docker stop my-container1 my-container2 my-container3
```

`docker stop`命令类似于`docker kill`命令，但是`docker stop`更友好，允许容器中的进程优雅地关闭，而`docker kill`立即发送 SIGKILL 信号，不给容器中的进程清理的机会。

通常认为使用`docker stop`是最佳实践，除非你出于某种原因需要立即杀死一个容器。

## 码头开始

与`docker stop`命令非常相似，这个命令用于启动一个或多个停止的 Docker 容器。

同样，要使用这个命令，您需要提供一个或多个容器 id 或名称。例如，如果您想要启动一个名为`my-container`的容器，您可以运行以下命令:

```
docker start my-container
```

要启动多个容器，您可以运行以下命令:

```
docker start my-container1 my-container2 my-container3
```

当您使用`docker start`命令启动一个容器时，该容器将以停止时的状态启动。

例如，如果您停止了一个正在运行 web 服务器的容器，用`docker start`启动该容器将重新启动 web 服务器，并使它在以前相同的端口上可用。

需要注意的是`docker start`命令只对处于停止状态的容器有效。如果您尝试启动一个已经在运行的容器，该命令将不会执行任何操作，该容器将保持运行状态。

要检查容器的状态，您可以使用`docker ps`命令，我们接下来会看到这个命令。

## docker ps

`docker ps`命令用于列出主机上正在运行的 Docker 容器。

当您运行此命令时，它将显示:

*   容器列表
*   他们的身份证
*   他们的名字
*   他们赖以建立的形象
*   正在使用的命令
*   它们开始的时间
*   以及他们的现状

例如，如果您的主机上运行两个容器，一个名为“web ”,另一个名为“database ”,您可以像这样使用`docker ps`命令:

```
$ docker ps

CONTAINER ID        NAME              IMAGE               COMMAND               CREATED             STATUS              PORTS               NAMES
a1b2c3d4e5f6        web               nginx               "nginx -g 'daemon…"   3 minutes ago       Up 3 minutes        80/tcp              web
b1c2d3e4f5g6        database          postgres            "postgres -c 'max…"   5 minutes ago       Up 5 minutes        5432/tcp            database
```

这对于管理和检查您的容器以及确保一切按预期运行非常有用。

根据您的具体需求,`docker ps`命令还有其他选项可以用来过滤和格式化输出。

## 码头经理

这允许您在正在运行的 Docker 容器中执行命令，比如 shell 提示符，而不必停止容器或创建新的容器。

例如，如果您有一个名为“web”的容器在您的主机上运行，并且您想在容器中打开一个 shell 提示符，您可以像这样使用`docker exec`命令:

```
$ docker exec -it web /bin/bash
```

**注:***`*-it*` *选项用于交互终端。**

*有点像当您使用 SSH 登录到远程服务器时，这个命令会在“web”容器中打开一个 shell 提示符，允许您运行命令并与容器交互，就像您直接登录一样。*

*除了运行命令之外，它还可以用于向正在执行的命令传递参数。例如，如果您想在“web”容器中运行`ls`命令来列出当前目录中的文件，您可以像这样使用`docker exec`命令:*

```
*$ docker exec web ls*
```

*这是一个非常强大的工具，用于管理正在运行的 Docker 容器并与之交互，因为它允许您在容器内运行命令，而无需停止或重新启动容器，这可以节省时间，并使使用容器变得更容易。*

*这些只是 Docker 中许多可用命令中的一部分。*

*要查看命令的完整列表，您可以不带任何参数运行`docker`命令，或者直接查看 Docker 文档。*

*[](https://docs.docker.com/engine/reference/commandline/cli/) [## 使用 Docker 命令行

### 要列出可用的命令，要么不带参数运行 docker，要么执行 docker help:取决于您的 Docker…

docs.docker.com](https://docs.docker.com/engine/reference/commandline/cli/)* 

# *结论*

*这是 Docker 和它的一些命令如何工作的基本概念。*

*当然，您还可以探索许多更高级的特性和选项，但这应该会给您一个使用 Docker 的良好起点。*

# *参考*

*[](https://docs.docker.com/engine/reference/builder/) [## Dockerfile 文件参考

### Dockerfile 文件的格式如下:指令不区分大小写。然而，惯例是让他们…

docs.docker.com](https://docs.docker.com/engine/reference/builder/) [](https://docs.docker.com/engine/reference/commandline/cli/) [## 使用 Docker 命令行

### 要列出可用的命令，要么不带参数运行 docker，要么执行 docker help:取决于您的 Docker…

docs.docker.com](https://docs.docker.com/engine/reference/commandline/cli/) 

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)*

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。**