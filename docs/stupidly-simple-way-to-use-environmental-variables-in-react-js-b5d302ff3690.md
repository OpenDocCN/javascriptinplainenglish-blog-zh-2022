# 在 React 中使用环境变量的简单方法

> 原文：<https://javascript.plainenglish.io/stupidly-simple-way-to-use-environmental-variables-in-react-js-b5d302ff3690?source=collection_archive---------6----------------------->

![](img/8b7b46ba777e910836e089c0b20830a4.png)

Photo by [visuals](https://unsplash.com/@visuals?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

环境变量是可以传递给程序运行时执行的值。它们通常用于配置应用程序的不同方面，例如数据库连接字符串或 API 端点 URL。在 React.js 中，环境变量可用于在不同的环境中配置应用程序，如开发、试运行和生产。

要在 React.js 中使用环境变量，首先需要在项目的根目录下创建一个`.env`文件。该文件将包含您希望在应用程序中使用的环境变量。值得注意的是，这个文件不应该被提交到版本控制，因为它可能包含敏感信息，如 API 密钥或数据库凭证。

在`.env`文件中，您可以使用`NAME=VALUE`语法定义您的环境变量。例如:

```
REACT_APP_API_ENDPOINT=https://my-api.com/
REACT_APP_DATABASE_USERNAME=my_username
REACT_APP_DATABASE_PASSWORD=my_password
```

前缀`REACT_APP_`很重要，因为它告诉 React 该变量将在您的应用程序中使用。

一旦在`.env`文件中定义了环境变量，就可以使用`process.env`对象在 React 组件中访问它们。例如，如果你想访问`REACT_APP_API_ENDPOINT`变量，你可以使用下面的代码:

```
const apiEndpoint = process.env.REACT_APP_API_ENDPOINT;
```

重要的是要注意到在`.env`文件中定义的环境变量只在开发模式下可用，在生产中不可访问。这意味着如果您想在生产中使用环境变量，您需要在您的生产环境中定义它们。

一种方法是使用`dotenv`包，它允许您在`.env`文件中定义环境变量，并在运行时将它们加载到您的应用程序中。要使用`dotenv`包，首先需要使用 npm 安装它:

```
npm install dotenv
```

一旦安装了`dotenv`包，您就可以通过调用`config()`方法从`.env`文件中加载您的环境变量。这应该在应用程序的入口点完成，比如`index.js`文件:

```
import dotenv from 'dotenv';
dotenv.config();
```

从`.env`文件加载环境变量后，您可以使用`process.env`对象在 React 组件中访问它们，就像之前一样。

总之，环境变量是在不同环境中配置 React.js 应用程序的有用方法。通过使用一个`.env`文件和`dotenv`包，您可以轻松地在 React 组件中访问和使用这些变量。这可以帮助您管理应用程序的配置，并使 API 键和数据库凭证等敏感信息不受版本控制。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*******

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***