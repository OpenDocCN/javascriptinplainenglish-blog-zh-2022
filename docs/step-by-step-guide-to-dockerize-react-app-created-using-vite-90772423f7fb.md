# 使用 Vite 创建的 Dockerize React 应用程序的分步指南

> 原文：<https://javascript.plainenglish.io/step-by-step-guide-to-dockerize-react-app-created-using-vite-90772423f7fb?source=collection_archive---------1----------------------->

反应|对接|邀请

![](img/f8d38039322b6524c11325eec145bb78.png)

> *最初发布于—*[*https://www . nandhakumar . io/post/step-by-step-guide-to-dockerize-vite-react-app-in-dev-environment*](https://www.nandhakumar.io/post/step-by-step-guide-to-dockerize-vite-react-app-in-dev-environment)

嘿伙计们！

在这篇文章中，您将学习如何将使用 Vite 工具为开发环境创建的 react 应用程序 dockerize

# 先决条件

*   React 的基础知识
*   对 docker 有基本的了解(我也会简单介绍一下)
*   本地系统上的 Docker

# Docker 是什么？

Docker 是一个帮助创建开发、测试和生产的公共环境(在 docker 世界中称为**容器**)的工具。

假设您正在本地环境中开发一个 react 应用程序(开发)

现在，一旦您完成了开发，您需要将源代码移交给测试团队，如果测试团队没有与您的本地环境相同的环境，可能会有一些问题会阻碍测试。

生产也有类似的情况。

那么，我们如何将环境运送到您运行应用程序的所有地方呢？

Docker 来了，它将为您的应用程序创建一个虚拟的运行环境，您可以在任何需要运行应用程序的地方创建和使用该环境。

很棒吧？

这是 Docker 的一个简短摘要。

如果你想了解更多，请查看官方 Docker 网站

现在让我们来看看如何对 React 应用程序进行 Dockerize。

# 步骤 1:使用 Vite 创建 react 应用程序(如果您已经有 React 应用程序，请跳过这一步)

```
npm create vite@latest
```

你会被要求

*   应用名称
*   使用哪种框架，如 React、Angular 或 Vue？选择反应
*   然后，Typescript 或者 Javascript。如你所愿选择

![](img/5e817d6cb119464e0bbb040fcd91ef08.png)

Vite Project Initialization

现在切换到项目目录

```
cd [your project name]
```

# 第二步:更新`vite.config`文件

这一步是在 Docker 容器和 React 应用程序之间映射端口所必需的

现在替换`vite.config`中的这段代码

```
export default defineConfig({
  plugins: [react()],
})
```

到

```
export default defineConfig({
  plugins: [react()],
  server: {
    watch: {
      usePolling: true,
    },
    host: true, // needed for the Docker Container port mapping to work
    strictPort: true,
    port: 5173, // you can replace this port with any port
  }
```

# 步骤 3:创建 Dockerfile 文件

在项目目录的根目录下创建一个名为`Dockerfile`的文件，如下所示👇

![](img/9940a51ffb55352689cdd760bc119449.png)

# 步骤 4:向 Dockerfile 添加命令

将这些命令复制到您的 docker 文件中

```
FROM node
WORKDIR /app
COPY package.json .
RUN npm i
COPY . .
## EXPOSE [Port you mentioned in the vite.config file]
EXPOSE 5173
CMD ["npm", "run", "dev"]
```

如果您不知道这些命令是什么，请阅读解释👇

*   `FROM node` -将在容器中创建一个节点环境
*   `WORKDIR /app` -将创建一个目录应用程序并切换到该目录
*   `COPY package.json .` -将 package.json 文件复制到/app 目录
*   `RUN npm i` -运行`npm install`为你的应用程序创建 node_modules
*   `COPY . .` -将源代码复制到/app 目录
*   `EXPOSE 5173` -打开端口，从容器外部(即浏览器)访问应用程序
*   `CMD ["npm", "run", "dev"]` -执行`npm run dev`启动服务器

# 步骤 5:构建 Dockerfile 文件

在终端中，导航到您的项目目录，然后执行

`!! Remove the [ ] when executing`

```
docker build -t [any name] .
```

**命令中使用的标志**

*   `-t` -标记集装箱(这将是您的集装箱名称)

构建完成后，将创建一个 docker 映像。

Docker 图像是运行容器的模板。

要检查您的 Docker 映像，请执行

```
docker images
```

它将显示您系统上可用的图像列表

检查运行`docker build`命令时给出的图像名称是否在列表中。

# 步骤 6:运行 Docker 容器

在终端中执行该命令👇

`!! Remove the [ ] when executing`

```
docker run -d --rm -p 5173:5173 --name [name of the container] [your docker image name]
```

**命令中使用的标志**

*   `-d` -在后台运行容器(分离模式)
*   `--rm` -删除容器，当你停止容器时
*   `-p` -集装箱与外界之间的端口映射。
*   `5173:5173` -【从浏览器访问端口】:【从容器中暴露的端口】

要检查 docker 容器是否正在运行，请执行

```
docker ps
```

它将显示在您的系统上运行的容器列表

检查运行`docker run`命令时给出的容器名称是否在列表中。

# 步骤 7:在浏览器中打开应用程序

打开浏览器并访问`http://localhost:[Port you mentioned in the docker run command]`，根据我们目前所做的配置，它应该是`[http://localhost:5173](http://localhost:5173)`

![](img/29ce4d8e1262da35bde17f95d0eb1720.png)

# 感谢阅读！

希望你今天学到了新东西😊。

在 [Twitter](https://twitter.com/nandhakumar_io) 、 [Instagram](https://www.instagram.com/nandhakumar.io/) 、 [Email](https://mailto:rsnk2013@gmail.com/) 和 [LinkedIn](https://www.linkedin.com/in/nandhakumar-dev/) 上关注并联系我，了解更多类似的有趣内容。

我的个人博客 [nandhakumar.io](https://www.nandhakumar.io/)

干杯✌️

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW)**** ***对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。*****