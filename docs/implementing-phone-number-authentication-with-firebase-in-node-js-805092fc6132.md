# 在 Node.js 中用 Firebase 实现电话号码认证

> 原文：<https://javascript.plainenglish.io/implementing-phone-number-authentication-with-firebase-in-node-js-805092fc6132?source=collection_archive---------0----------------------->

![](img/b60d6444f0075f0b43052767c9fd2cbf.png)

Image by [Thomas Ulrich](https://pixabay.com/users/lobostudiohamburg-13838/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=292994) from [Pixabay](https://pixabay.com//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=292994)

电话号码**认证**是一种流行的登录应用程序的方法，因为它允许用户使用他们的电话号码作为他们的身份，而不是用户名和密码。在本教程中，我们将了解如何使用 Firebase 来验证 Node.js 应用程序中的电话号码。

**Firebase** 是一个开发 web 和移动应用的流行平台，它包括一个**实时数据库**、**云存储**和**用户认证。**Firebase 提供的电话号码认证 API 使开发人员能够简单地将电话号码认证添加到他们的应用程序中，而不必构建他们自己的认证系统。

首先，我们将创建一个 Firebase 帐户，并配置一个 Node.js 应用程序来利用 Firebase。然后，我们将讨论如何在 Node.js 应用程序中使用 Firebase 实现电话号码认证。学完本课程后，您将拥有一个可以在自己的应用程序中使用的电话号码认证系统。我们开始吧！

## 步骤 1:设置 Firebase 帐户

1.  进入 Firebase 网站([https://firebase.google.com/](https://firebase.google.com/))，点击**免费入门**按钮。
2.  使用您的 Google 帐户登录。如果您还没有 Google 帐户，您必须在开始之前创建一个。
3.  要启动一个新的 Firebase 项目，请单击**添加项目**按钮。
4.  在按下**创建项目**按钮之前，为您的项目命名并选择一个区域。
5.  允许谷歌分析如果你想看到分析，这一步是可选的。
6.  项目创建完成后，您将被带到 Firebase 控制台。您可以从这里访问许多 Firebase 服务，比如实时数据库、云存储和身份验证。
7.  在 Firebase 控制台中，从左侧菜单中选择**认证**。
8.  选择**设置签到方式**选项。
9.  点击**电话**标题下的**启用**按钮。
10.  要为 Firebase 项目配置电话号码身份验证，请按照提示进行操作。
11.  如果您的应用程序的域名未列在**授权的** **域中，请添加该域名。**
12.  转到项目设置->常规->在代码中保存 API 键。

完成这些步骤后，您的 Firebase 帐户就可以用于电话号码认证了。之后，您可以将 Firebase 连接到 Node.js 应用程序。

## **第二步:与 Node.js 集成**

安装 Firebase Node.js 客户端库，并配置您的项目使用 Firebase 将 Firebase 电话号码身份验证集成到您的 Node.js 应用程序中。您可以采取以下措施来实现这一目标:

1.  按如下方式安装 Firebase 客户端库:可以通过执行以下命令，使用 npm 安装 Firebase 客户端库:

```
npm install firebase
```

2.创建一个 Firebase 项目:如果你还没有，你需要创建一个并激活电话号码认证。为此，请遵循上一步中概述的步骤。

3.获取 Firebase 项目的凭据:要在 Node.js 应用程序中使用 Firebase，必须首先获取 Firebase 项目的凭据。

为此，导航至 Firebase 界面并选择右上角的**设置**图标(齿轮图标)。
二。在**项目** **设置**页面点击**通用**标签，然后点击**添加 app** 按钮。
三。要向 Firebase 项目添加 web 应用程序，请按照提示进行操作。这将为您提供一组在配置 Node.js 应用程序时使用的凭证。

4.启动 Firebase 客户端库:要在 Node.js 应用程序中使用 Firebase，必须首先通过调用`initializeApp`函数初始化 Firebase 客户端库，并为它提供 Firebase 项目的凭证。这里有一个你可以如何去做的例子:

```
const firebase = require('firebase');

const firebaseConfig = {
  apiKey: 'API_KEY',
  authDomain: 'AUTH_DOMAIN',
  databaseURL: 'DATABASE_URL',
  projectId: 'PROJECT_ID',
  storageBucket: 'STORAGE_BUCKET',
  messagingSenderId: 'MESSAGING_SENDER_ID',
  appId: 'APP_ID'
};

firebase.initializeApp(firebaseConfig);
```

5.使用 Firebase 身份验证服务:要在 Node.js 应用程序中集成电话号码身份验证，请使用 Firebase 身份验证服务。这里有一个你可以如何去做的例子:

```
// Require the Firebase client library
const firebase = require('firebase');

// Get the authentication service
const auth = firebase.auth();

// Send a verification code to the user's phone
auth.sendSignInLinkToPhoneNumber(phoneNumber, actionCodeSettings)
  .then(function() {
    // The verification code has been sent to the user's phone
  })
  .catch(function(error) {
    // An error occurred while sending the verification code
  });

// Sign the user in using the verification code they received on their phone
auth.signInWithPhoneNumber(phoneNumber, verificationCode)
  .then(function(result) {
    // The user has been signed in
  })
  .catch(function(error) {
    // An error occurred while signing the user in
  });
```

这个例子演示了如何向用户的手机发送一个验证码，然后使用这个验证码让用户登录。在 Node.js 应用程序中实现电话号码身份验证时，Firebase 身份验证服务还有更多的功能可供使用。

我希望这有所帮助！*感谢您的阅读。*

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*