# 如何使用 React 执行 Google 登录

> 原文：<https://javascript.plainenglish.io/how-to-perform-google-authentication-with-react-7d43fb0e4922?source=collection_archive---------2----------------------->

## 使用 React 实现 Google OAuth2

![](img/44a11b0f334c6a4f666bad1cd8f09828.png)

Photo by [Kevin Ku](https://unsplash.com/@ikukevk?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

如果我们需要与任何 Google 服务进行交互，或者只是使用 Google 对用户进行身份验证，我们必须使用 Google 实现身份验证机制。一些使用案例可能是:

*   使用 React 将文件上传到 Google drive
*   从 React 与 YouTube API 交互
*   React 中与 Google sheets 的交互

为了实现这一点，我们已经有了一个很好的库，叫做[，用谷歌](https://www.npmjs.com/package/react-google-login)登录。让我们看看如何利用这一点。

首先，安装依赖项:

```
yarn add react-google-login
```

# 先决条件

你需要在[谷歌云](https://console.cloud.google.com/)上拥有一个账户。如果您还没有，请先创建一个免费帐户，然后继续。

您还需要一个谷歌云项目，并从凭据仪表板获取 CLIENT_ID。我想你已经有了。

# 使用谷歌登录

然后导入 GoogleLogin 并在代码中使用它。

```
import React from "react";
import { GoogleLogin } from "react-google-login";const CLIENT_ID = "YOUR_CLIENT_ID_HERE";function Login() {
  const responseGoogle = (response: any) => {
    console.log(response.accessToken);
  };
  return (
    <div className="App">
      <GoogleLogin
        clientId={CLIENT_ID}
        buttonText="Login"
        onSuccess={responseGoogle}
        onFailure={responseGoogle}
        cookiePolicy={"single_host_origin"}
      />
    </div>
  );
}export default Login;
```

如果登录成功，您将在响应对象中获得一个`accessToken`和一个`tokenId`。将令牌保存在状态变量之类的东西中。您可以使用此 accessToken 进一步调用其他服务。

# 注销

我们也可以使用这个库实现注销功能。

```
import { GoogleLogout } from "react-google-login";function Logout() {
  const logoutHandler = () => {
    console.log('successfully logged out!);
  };
  return (
    <GoogleLogout
      clientId={CLIENT_ID}
      buttonText="Logout"
      onLogoutSuccess={logoutHandler}
    />
  );
}export default Logout;
```

在实际应用中，我们希望根据身份验证状态来使用这两种特性。我们可以结合这两个特性来跟踪登录状态并显示适当的组件。

最终的代码看起来会像这样。

你会注意到我们在这里引入了一个名为`scope`的新变量。为了调用像 YouTube API 或 Google Drive API 这样的服务，我们必须在这里定义作用域。

你可以从 [OAuth2 游乐场](https://developers.google.com/oauthplayground/)拿到望远镜。

## 例子

```
GOOGLE_DRIVE_SCOPE = "https://www.googleapis.com/auth/drive";
YOUTUBE_DATA_API_V3 = "https://www.googleapis.com/auth/youtube";
```

今天到此为止！希望你学到了新的东西！

```
**Want to Connect?**You can reach out to me via [**LinkedIN**](https://www.linkedin.com/in/56faisal/) or my [**Personal Website**](https://www.mohammadfaisal.dev/blog)
```

# Github 回购

[](https://github.com/Mohammad-Faisal/react-google-authentication-demo) [## GitHub-Mohammad-fais al/react-google-authentic ation-demo:使用 ReactJS 的 Google 认证演示

### 如果我们需要与任何谷歌服务进行交互，或者只是使用谷歌认证用户，我们必须实现…

github.com](https://github.com/Mohammad-Faisal/react-google-authentication-demo) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*