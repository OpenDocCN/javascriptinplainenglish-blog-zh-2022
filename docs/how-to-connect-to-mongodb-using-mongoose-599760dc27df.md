# 如何使用 Mongoose 连接到 MongoDB

> 原文：<https://javascript.plainenglish.io/how-to-connect-to-mongodb-using-mongoose-599760dc27df?source=collection_archive---------9----------------------->

## 关于如何使用 Mongoose 连接到 MongoDB 的教程

![](img/168cffe0b8e61f435bfed58b848b068a.png)

Photo by [Uriel SC](https://unsplash.com/@urielsc26?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

MongoDB 是一个用于存储数据的 NoSQL 数据库。使用 node，您可以创建一个连接到远程 MongoDB 服务器的服务器，并创建数据库集合来存储不同类型的数据。

Mongoose 使得连接到 MongoDB 变得非常简单，并且内置了对模型和数据类型的支持。

第一步是安装 Mongoose 和其他依赖项。下面是我的 package.json 文件，其中包含本例中的所有依赖项:

```
{"name": "node-mongoose","version": "1.0.0","description": "","main": "app.js","dependencies": {"bcryptjs": "^2.4.3","body-parser": "^1.20.0","ejs": "^3.1.8","express": "^4.18.1","express-session": "^1.17.3","mongoose": "^6.4.3","nodemon": "^2.0.18"},"scripts": {"start": "nodemon app.js","example": "nodemon example.js","test": "echo \"Error: no test specified\" && exit 1"},"keywords": [],"author": "","license": "ISC"}
```

只需复制这个文件并运行 npm install，就可以在 Node.js 终端中使用 npm run start 运行服务器。

```
const mongoose = require('mongoose')
```

一旦导入了 Mongoose，就可以创建一个模式或模型。

```
const postSchema = new mongoose.Schema({ title: { type: String, required: true }, content: {
        type: String, required: true }
})module.exports = mongoose.model('Post', postSchema)
```

一旦创建了这个模型，您就可以读取、写入和更新这个集合中的文档。集合名称将作为“文章”存储在数据库中。

要连接到 MongoDB 数据库，您需要一个连接字符串，它在您的 MongoDB Atlas 主机上提供。该连接字符串包括数据库名称和密码，因此请确保将其安全地存储在. env 文件中。

```
const CONNECT_URL = "" // Your connection string
mongoose.connect(CONNECT_URL, { useNewUrlParser: true, useUnifiedTopology: true }).then((result) *=>* {// If connection is successful, start the server.app.listen(process.env.PORT || 8000);}).catch((error) *=>* {console.log(error);});
```

一旦添加了连接，就可以开始添加 GET 和 POST 路由来处理不同的请求。

为了处理路由，我将使用 express。

```
*const* express = require("express");
*const* app = express();
```

为了渲染这个例子中的页面，我将使用 EJS 作为模板引擎。用 npm 安装 EJS，然后添加 EJS 作为默认模板引擎。

```
app.set("view engine", "ejs");app.set("views", "views");
```

我将在主文件夹中创建一个名为 views 的文件夹，在这个文件夹中，我将添加一个 posts.ejs 文件。在主页上，我将从数据库集合中获取文章，并将它们呈现到模板 posts.ejs 中。

```
app.get("/", (req, res) => {

    const Post = mongoose.model("Post", postSchema); Post.find().then(posts => { res.render("posts", {posts: posts}) })})
```

posts 数组将被传递给 posts.ejs 模板，在这个模板中，您可以使用特殊的语法来呈现帖子。

```
<% posts.map(post => { %> <div><%= post.title %></div><% }) %>
```

完整的文件如下所示:

```
<html lang="en"><head><meta charset="UTF-8" /><meta http-equiv="X-UA-Compatible" content="IE=edge" /><meta name="viewport" content="width=device-width, initial-scale=1.0" /><title>Home</title></head><body><h2>Posts</h2><% posts.map(post => { %><div><%= post.title %></div><% }) %></body></html>
```

为了在 EJS 中执行 JavaScript，该语法打开和关闭 JavaScript 代码，并执行其中的代码:

```
<% %>
```

要呈现 JavaScript 变量的值，使用以下语法:

```
<%= %>
```

最后，如果您想要创建模板文件，您可以使用以下标记来呈现它们:

```
<%-  %>
```

# 源代码

这就是了。感谢您的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**