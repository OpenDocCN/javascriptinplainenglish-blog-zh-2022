# 使用 Express 创建 Node.js 应用程序

> 原文：<https://javascript.plainenglish.io/create-a-node-js-app-with-express-fcc7fac94687?source=collection_archive---------7----------------------->

## 使用快速和 EJS 渲染一个网站。

![](img/824e580666250c052e7afc26ba2e8511.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/es/@juanjodev02?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Express 使创建服务器和渲染不同路线变得更加简单。和 EJS 一样，它让网络开发变得轻而易举。Express 处理文件、路由、解析等等。

首先，用 npm init 设置 Node.js 项目，或者复制文章末尾提供的 package.json 文件。

然后，运行 npm install 在 package.json 文件中安装依赖项。在 app.js 文件中，导入 express 以开始设置服务器和路线。

```
const express = require('express')const app = express()
```

您还需要将 EJS 设置为模板引擎，并链接到视图文件夹，以便让 express 知道视图模板的位置。

```
app.set('view engine', 'ejs')app.set('views', 'views')
```

设置路由的一个简单方法是使用`app.get()`来获取请求。

```
app.get("/", (req, res) => { res.render("index")})
```

最后，在端口 3000 上设置服务器。

```
app.listen(3000)
```

现在您可以转到 localhost:3000 并查看结果。第二条路由应该位于 localhost:3000/ejs。

# 源代码

现在你知道了。感谢您的阅读。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*