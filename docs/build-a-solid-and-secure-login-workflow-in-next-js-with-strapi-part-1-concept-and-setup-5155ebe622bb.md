# 使用 Strapi 在 NextJS 中构建一个可靠且安全的登录工作流

> 原文：<https://javascript.plainenglish.io/build-a-solid-and-secure-login-workflow-in-next-js-with-strapi-part-1-concept-and-setup-5155ebe622bb?source=collection_archive---------3----------------------->

## 第 1 部分:用 NextJS 和 Strapi 构建可靠、安全和可伸缩的登录系统的概念和设置。

![](img/bf8690525d89572b9a1dc4806a65658a.png)

在过去的 3 个月里，我们使用[Strapi](https://medium.com/u/ace2e82e28e6?source=post_page-----5155ebe622bb--------------------------------)(【https://strapi.io/】T2)作为后端，在 NextJS 中从零开始构建了一个完整的电子商务，在这个开发过程中，我们遇到了一些问题，我们需要大量的试验和错误来实现我们一直在寻找的行为，因为 Strapi(尤其是 v. 4)并不总是很好地正确记录。无论如何，我们能够克服困难，我们记录了我们的发展道路。和我们的项目一样，我们从最烦人的任务开始:**构建一个可靠、安全、可伸缩、可靠和可重用的登录工作流**

Strapi 提供了一个内置的用户管理和登录系统，可以通过社交登录进行扩展。不幸的是，大部分教程都涉及了这个系统与外部库的使用(例如 [next-auth](/passwordless-authentication-in-next-js-with-nextauth-js-and-mongodb-19760c79184) )，并且文档并不总是与 v. 4 保持同步，所以我们决定在本教程中分享我们的经验。

由于构建生产就绪的登录系统是一项漫长而复杂的任务，我们将本教程分为 3 个部分:

*   第 1 部分:概念和设置
*   [第 2 部分:注册和登录](https://popeating.medium.com/build-a-solid-and-secure-login-workflow-in-next-js-with-strapi-part-2-register-and-login-4971cc7176f5)
*   [第 3 部分:社交登录和密码重置](https://popeating.medium.com/build-a-solid-and-secure-login-workflow-in-next-js-with-strapi-part-3-social-login-and-password-7409bfad28fb)

您还可以下载或克隆这个项目的存储库，以便跟进:

[](https://github.com/popeating/fullcomm) [## GitHub - popeating/fullcomm

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/popeating/fullcomm) 

## 基本概念

Strapi 提供开箱即用的用户注册和登录功能(两者都使用社交网络提供商)。Strapi API 为所有主要的登录任务(注册、登录、密码提醒等等)公开端点，一旦用户通过身份验证，Strapi 提供一个 JWT，可以用于所有其他可能需要它的请求(例如，在我们的例子中，通过身份验证的用户可以查询订单以获得他们过去的订单列表，或者通过身份验证的用户可以访问特殊优惠，情况是无限的)。它还提供了通过电子邮件确认注册的能力(我们使用了一部分，但在本教程中也有)。

如前所述，在成功登录后，Strapi 向客户端发送回一个 JWT，如果我们想要持久化我们的会话，我们需要存储它，并且我们需要将它安全地存储在一个 httpOnly cookie 中([更多关于 http only cookie](https://indepth.dev/posts/1382/localstorage-vs-cookies))，这样它就可以被(例如)getServerSideProps 访问。HttpOnly cookies 只能由服务器设置，所以我们需要在我们的前端和 Strapi 后端之间有一个中间件来处理它。我们选择 NextJS 中包含的 [API 路由，并且我们还使用了一个上下文来集中每个与登录相关的功能和状态。](https://nextjs.org/docs/api-routes/introduction)

起初看起来很复杂，但是(在我们看来)这是处理登录过程最有效和最安全的方式。最基本的工作流程如下:

*   带有登录表单的组件将通过上下文函数发布数据
*   上下文函数将获取数据，并将其发送到 NextJS API
*   NextJS API 将数据发送给 Strapi API
*   Strapi API 验证数据并回复 NextJS API(让我们假设这是一次成功的登录)
*   NextJS API 读取响应，设置 httpOnly cookie，并将确认发送回上下文
*   初始组件用登录的数据重新组合(或重定向到某个地方)

## 工具和先决条件

我们试图使用最少的库来开发这个项目，对于我们使用的前端(除了 NextJS):

*   [axios](https://www.npmjs.com/package/axios) (访问 API)
*   [react-hook-form](https://react-hook-form.com/) (验证和管理表单)
*   [cookie](https://www.npmjs.com/package/cookie) (解析并序列化 cookie)
*   [顺风 CSS](https://tailwindcss.com/) (造型用)

对于后端，我们只使用了全新安装的 Strapi v4

要跟进这个项目，您需要:

*   良好的 React 和 NextJS 知识
*   对反应环境有很好的理解，
*   熟悉 NextJS API 路线
*   Strapi 的基本知识
*   顺风 CSS 的基础知识
*   对登录工作流程有很好的了解
*   已安装 SQLite 数据库

## 安装和配置 Strapi

我们将 Strapi 和 NextJS 安装在同一个本地机器上，但是它可以稍后部署在不同的服务器上，或者部署在具有不同端口或域名的同一台服务器上。

使用默认的 SQLite 数据库安装 Strapi 的[新副本](https://docs.strapi.io/developer-docs/latest/getting-started/quick-start.html)

```
**npx create-strapi-app@latest my-project --quickstart**
```

安装完成后，打开地址`http://localhost:1337/admin`并配置您的用户。

转到设置->高级设置:

![](img/e0ff591d9765c91e166bccba478b0e8f.png)

并激活“启用注册”和“启用电子邮件确认”，还将*重置密码页面*设置为`http://localhost:3000/user/resetpassword`并将*重定向 url* 设置为`http://localhost:3000/user`(稍后将详细介绍)。

接下来，转到设置->角色，并选择公共:

![](img/ed4b037145beda680122edfcaa3591c5.png)

在*授权*部分选择*用户-权限*并全部启用。
返回角色并选择已验证:

![](img/e352baef3281270c2bf654d3ce376b88.png)

在*用户权限*部分至少为用户启用“me”端点

为 Strapi 配置电子邮件插件，您需要创建(或者编辑，如果已经存在的话)一个配置文件`/config/plugin.js`。

这是我们使用 sendmail 的配置(你可以在[https://docs . strapi . io/developer-docs/latest/plugins/email . html # configure-the-plugin](https://docs.strapi.io/developer-docs/latest/plugins/email.html#configure-the-plugin)上找到更多关于配置电子邮件插件的信息)。
请务必添加真实的电子邮件地址

服务器重新启动后，通过进入设置->电子邮件插件->配置并发送测试电子邮件来检查配置是否正常:

![](img/a5dbcfb8508ac15c527bd46fe6709dc1.png)

您还需要在设置->电子邮件模板中配置电子邮件模板。您应该配置一个真实的电子邮件地址，以便一切正常工作。

![](img/ce41aa2d2239cec7b9bc59d1f0bae7a4.png)

**配置谷歌登录**

如果您希望您的用户使用第三方提供商(如谷歌或脸书)登录，您需要在 Strapi 中使用您需要在登录提供商网站上获得的一些数据来配置它。在本指南中，我将展示如何配置谷歌登录和脸书登录，但基本上，每个供应商将遵循相同的模式。
进入[谷歌云平台](https://console.cloud.google.com/)，使用你的谷歌凭证登录或注册。
创建一个新项目，并随意命名(我们使用了 nextLogin):

![](img/390d05b3e42e3b309120a010b55bdd7c.png)

项目准备就绪后，选择它并转到 API & Services dashboard:

![](img/e13983cf527dce18abb8d1037f79c422.png)

配置 OAuth 同意屏幕，选择外部并填写所有必填字段，当请求时添加以下范围:。 */auth/userinfo.email* 和*。/auth/userinfo.profile，*保存，然后点击“发布应用”发布应用

![](img/775a9bcc19a31fb54ad3c73a5e0af2fa.png)

点击*凭证*创建凭证，然后点击*创建凭证*并选择 OAuth 客户端 ID

![](img/bffa1c0e48d2a22a7f5cae43d003522c.png)

填写必填信息，添加`http://localhost:1337/api/connect/google/callback`为授权重定向 URI

![](img/4aa56b9c106c71d3d4743fafc1ebebad.png)

保存并获取凭证(客户端 ID 和客户端密码)

![](img/6f10df37b51a7b7c4a9690746a224d82.png)

有了凭证，回到你的 Strapi 面板，进入设置->提供商并启用谷歌:

![](img/4d04cfc7d9337e63036a626318e05333.png)

粘贴客户端 ID、客户端密码，将重定向 URL 设置为`http://localhost:3000/user/googleCallback`(这将是 Strapi API 稍后使用 Google 提供的访问令牌调用的页面)，并检查您添加到云控制台的重定向 URL 是否与此处显示的相同。

**配置脸书登录**

脸书登录配置非常相似，你需要在 [Meta 上为开发者](https://developers.facebook.com/)创建一个新的消费应用(或者使用你已经有的应用)。

登录后，点击“创建应用”，然后选择“消费者”

![](img/74471b7735ae568985771098e063f805.png)

在表格中填写所需信息，然后选择“脸书登录”作为产品:

![](img/fa94f676c5ebac68606f080aee99742d.png)

在接下来的步骤中，选择 Web，将域设置为`http://localhost:3000`并保存，您现在可以点击菜单*设置- >基本*，在这里您可以获得您的应用 ID 和应用密码:

![](img/efe784ad4e2966d5e88283572c69d0b8.png)

一旦你得到了它们，回到 Strapi 并像你为 Google 所做的那样配置脸书:

![](img/903bf38ccf9802d641a1c060054524cf.png)

这次使用`http://localhost:3000/user/facebookCallback`作为你的重定向网址。

如果您需要配置更多的提供者，只需遵循这种模式:在提供者站点上创建密钥，将它们添加到 Strapi，如果提供者需要回调 URL，您可以在 Strapi 前端重定向 URL 中使用`http://localhost:1337/connect/[provider]/callback`
，使用类似于`http://localhost:3000/user/[provider]Callback`(每个提供者都需要一个这样的 URL)。

## 设置和配置 NextJS

我们从一个新的 NextJS 应用程序开始，使用这个命令创建一个应用程序(随意更改应用程序名称)

```
npx create-next-app fullcomm
```

安装所需的模块:

```
npm install axios
npm install cookie
npm install react-hook-form
```

安装和配置顺风 CSS:

```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
npm install @tailwindcss/forms
```

编辑 tailwind.config.js，如下所示:

清空文件`style/global.css`,添加以下几行:

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

清洁文件`pages/index.js`并保持如下状态:

删除`pages/api/hello.js`和`styles/Home.module.css`，从`pages/_app.js`中删除其引用

创建`.env.local`并向其添加以下行:

这样你应该有一个空白的画布来开始编码。
运行`npm run dev`如果一切正确，如果你打开地址`http://localhost:3000`你应该得到一个白色的页面，上面有家。

接下来，我们将准备一个用于初始化所有 axios 连接的实用程序，创建文件`lib/api.js`

我们基本上导出了两个初始化 axios 的函数，以连接到 Strapi ( *instance* )和连接到 NextJS API ( *linstance* )。每当我们需要获取或发送到 API 端点时，这两个连接将与我们的项目一起使用。

在我们开始编码之前，我们需要设置一个上下文([https://reactjs.org/docs/context.html](https://reactjs.org/docs/context.html))，它将包装我们所有的应用程序，这个上下文将保存所有的数据、状态、功能、偏好等等，这些都将对我们所有的页面和组件可用。

让我们从在`context/user.js`中创建一个空的提供者开始:

我们创建了一个 *dummy* 状态和一个 *dummyfunction* ，它们将可用于项目中的所有页面和组件，我们还导入了 *linstance* ，因为稍后我们将向需要它的提供者添加更多的函数(例如登录和注销函数)。
为了将提供者传播给所有孩子，我们需要将我们的应用程序包装在其中，这可以通过修改`pages/_app.js`，通过导入`UserProvider`并将应用程序包装在其中来实现:

我们选择将所有与用户相关的操作保存在一个上下文中，这样我们就可以在任何时候从任何组件中访问它们，不管它是如何嵌套的。例如，我们将在上下文中有一个函数，它将检查用户是否登录，每次我们需要时，可以从每个页面或单个组件调用它。我们还遵循一种设计，其中所有上下文函数在 *return* 中发送回复，并且不执行任何动作(如重定向或接口修改)，这样任何组件或页面都负责获得响应、对其进行处理并执行所需的动作。

在下一部分，我们将开始编写我们的应用程序，我们将允许用户注册到我们的网站，并在确认电子邮件地址后使用用户名(或电子邮件)和密码登录。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**