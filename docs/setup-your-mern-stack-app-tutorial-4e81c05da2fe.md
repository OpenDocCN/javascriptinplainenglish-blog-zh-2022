# 如何从头开始设置您的 MERN 应用程序

> 原文：<https://javascript.plainenglish.io/setup-your-mern-stack-app-tutorial-4e81c05da2fe?source=collection_archive---------1----------------------->

## 让我们全押吧

![](img/f9040d3593fc5ce70eb755ee5fdd1e9e.png)

在本教程中，我将快速浏览什么是 MERN，以及如何从头开始设置一个 MERN 应用程序。这也将是我未来文章的样板代码，所以请确保您正确理解了这一点。我计划在我即将到来的系列文章中写一系列的 MERN 堆栈项目教程。这将是开始的样板。

MERN 是一个 web 开发框架。单词 **MERN** 代表一组用于构建全栈应用的技术。是 **M** ongoDB、 **E** xpress、 **R** eact、 **N** ode.js 中第一个字母的集合

![](img/b7723933f2c21dcd3d7a174882b78a50.png)

任何全栈 web 应用程序都由 3 个主要组件组成:前端、后端和数据库。上图显示了 MERN 堆栈应用程序中 3 个组件之间的交互方式。

我们的 Node.js 应用程序将数据库和前端连接在一起。我们使用 Express 库来实现它

因此，我们将创建一个类似的 web 应用程序，包含所有 3 个主要组件。首先，让我们创建后端。它由服务器和连接到服务器的数据库组成。

在您的项目文件夹中，创建一个名为 **server** 的文件夹。所有与我们后端相关的文件和包都放在那里。在**服务器**文件夹中，加载一个 **cmd** 终端并运行以下代码。确保运行创建的**服务器**文件夹中的代码。

运行`npm init-y`并初始化一个包，json:

使用下面的代码安装软件包`mongoose,express,cors and dotenv`:

这些是我们安装的软件包。

**express:** 这是一个 Node.js web 框架/服务器框架，用于创建后端服务器和 API。

**mongose:**用于创建 MongoDB(我们的数据库)和 Express web 应用程序之间的连接。

**cors:** 用于跨产地资源共享。

**dotenv:** 安装从**加载环境变量的模块。env** 文件转换成 **process.env** 文件。您可以将用户名和密码等配置值从代码中分离出来，并单独处理它们。

在我们的**服务器**文件夹中创建一个名为 **server.js** 的文件，然后
将以下代码行添加到 **server.js** 中。我们将在下面讨论每一行的作用。

我们已经导入了 express 服务器，初始化了一个 express 实例，并将其分配给变量 app

我们已经导入了 cors，在第 5 行中，我们通过传递给应用程序来使用它。

我们已经导入了 mongoose，将来可以用它来连接数据库。

在第 6 行中，我们已经传递了内置的 express 中间件函数`express.json`。

该方法用于将带有 JSON 有效负载的传入请求传递给服务器。通过使用这种方法，我们可以像访问 JSON 对象一样使用点符号来访问传入的请求对象，例如`req.body.name`。

接下来，我们必须创建 MongoDB 连接 URL，并使用该 URL 来创建我们的 express server MongoDB 连接。

可以关注我的 [YouTube](https://www.youtube.com/watch?v=0Pt7Kfh78Jg&t=4s) 视频，学习如何轻松创建连接 URL。

一旦获得连接 URL。在项目中创建一个`config.env`文件，并添加连接 URL 和端口。

我的 config.env 看起来像这样。

```
ATLAS_URI=mongodb+srv://mydbname:08kDdtyghjYwN6fdp@cluster1.qhyh6.mongodb.net/hello?retryWrites=true&w=majority
PORT=5000
```

接下来，使用猫鼬和。env 文件连接到数据库。将以下代码块添加到 server.js 中

在上面的代码块中，在第 1 行，我们使用了`.dotenv`包，之后，我们可以使用 process.env 来访问 config.env 中的配置变量。

我们这样做是因为当我们将项目上传到服务器时，我们不上传 config.env。我们在服务器上单独设置这些值。当我们在服务器上运行代码时，我们的代码可以访问 process.env。

在我们运行服务器之前，修改一下`package.json`文件。在脚本下添加`"start": "node server.js"`。

![](img/8d54a3a927d162a9a40e43a25f9d891e.png)

最终 server.js 代码

在终端运行 `npm start`。

![](img/66257b464fb4e323c7008fc4b0dbcc26.png)

一旦数据库连接完成，让我们添加路线和控制器。

## 向服务器添加 API 端点

在本节中，我们将在 MERN 应用程序中添加一些虚拟控制器和路线。

首先，让我们在服务器中创建两个文件夹`routes`和`controllers`。
在控制器文件夹中，让我们创建第一个控制器。创建一个名为`profile.js`的文件，并添加下面的代码。

我们将添加一些控制器和路由，一旦调用特定的端点，它们将给出一个响应值。

我们在`profile.js`控制器中定义了两个函数并导出了它们。

接下来，我们将创建路由器，它将使用我们上面定义的控制器。
在 routes 文件夹中，创建一个`profile.js`文件。

使用快速创建路线的步骤如下。

1.  进口快递。
2.  创建快速路由器对象。
3.  从我们的控制器文件夹导入先前创建的`profile.js`控制器
4.  创建路由器并添加控制器函数作为回调来处理请求。
5.  导出路由，以便我们可以在 server.js 中使用它

使用 server.js 文件中的路由。

首先将路线导入到`server.js`文件中:

```
const profileRoutes=require('./routers/profile')
```

我们可以像这样使用`server.js`文件中导入的路由。

```
app.use('/',profileRoutes)
```

所以所有以`“/”`开头的 API 调用都在`profileroute`内部进行。

定稿`server.js`:

与邮递员一起测试:

您可以安装 Postman 并测试我们使用 Postman 创建的端点。

![](img/ba3e1e570d2d88efbab81ae3afc25a13.png)

它成功地工作了。

现在我们已经完成了后端，让我们开始创建我们的前端反应应用程序。

## 设置 react 应用程序

在客户端文件夹中，运行:

```
npx create-react-app .
```

或者

在主项目文件夹中，运行:

```
npx create-react-app client
```

上面的代码将创建一个名为 client 的独立文件夹，并在其中安装 React 库。

接下来，在我们的 React 项目中安装 axios。

```
npm i axios --save
```

在 react `package.json`内部，在末尾添加代理值。

```
"proxy": "http://127.0.0.1:5000"
```

这将把我们所有的前端 API 调用重定向到运行在端口 5000 的服务器。

![](img/b78dd0f57634a34f3b4c13797069b088.png)

在 React 项目中，让我们创建第一个 API 调用。

编辑`app.js`如下:

我们已经声明了一个名为`getData`的异步函数，并在`useEffect`内部调用了它。

`getData`函数使用 Axios 调用 API，并使用 useState 钩子设置响应值。我们可以在前端看到检索到的消息。

因此，基本上在这个项目中，我们从前端向后端发送一条消息，从后端获得响应，并在我们的 React 前端中显示它。

最终代码可以在 GitHub repo 中找到:
[https://github.com/Lahirutech/MERN_boilerplate](https://github.com/Lahirutech/MERN_boilerplate)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*