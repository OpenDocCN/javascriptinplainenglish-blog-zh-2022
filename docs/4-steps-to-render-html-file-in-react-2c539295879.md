# 在 React 中呈现 HTML 文件的 4 个步骤

> 原文：<https://javascript.plainenglish.io/4-steps-to-render-html-file-in-react-2c539295879?source=collection_archive---------6----------------------->

![](img/0e28f8993dabc68bcfad6d28ff3a50cf.png)

# 1.

我正在使用 Next.js 库，所以您需要安装它。[如果你是新手，下面是入门链接](https://www.youtube.com/watch?v=Mmamf4_It9c)。

[](https://medium.com/nerd-for-tech/you-really-need-to-migrate-to-next-js-ee646a9982ab) [## 你真的需要迁移到下一个 JS

### 这是原因，为什么？

medium.com](https://medium.com/nerd-for-tech/you-really-need-to-migrate-to-next-js-ee646a9982ab) 

# 2.

一旦安装了存储库，我们将处理无服务器功能(如果是新的，则为[)，然后向无服务器功能添加以下代码。](/serverless-function-in-next-js-3cd0d22ab983)

我正在 pages/api 目录中创建一个示例 hello API，它将返回一个 HTML 文件作为响应。

```
import fs from "fs";const filename = "/portfolio/index.html";module.exports = async(*req*, *res*) => {
 *res*.setHeader("Content-Type", "text/html, charset=utf-9");
 *res*.write(await fs.readFileSync(filename, "utf-8"));
 *res*.end();
};
```

# 3.

添加 HTML 文件是第三步。

根目录中的`pages`目录是 next.js 存储库中所有静态文件的位置。

将 HTML 代码添加到`profile.html`文件中。

```
<html>
    <head>
        <title>Example</title>
    </head>
    <body>
        <p>This is an example of a simple HTML page with one  paragraph.</p>
    </body>
</html>
```

# 4.

这是至关重要的一步，我们现在将告诉 next.js 显示渲染 index.html 文件中的 HTML 代码，并将它们返回到`api/profile`页面。

当用户打开个人资料页面时，`api/profile`端点将收到在网站上呈现`profile` HTML 文件的请求。

我们将告诉 next.js 使用代理 URL 概念配置请求，这将通过在根目录的`next.config.js`文件中添加后续代码来实现。

```
module.exports = () => {
 rewrites: async () => [{
  source: "/public/portfolio/index.html",
  destination: "/pages/api/portfolio.js",
 },],
}
```

现在我们的 profile.html 路线将简单地呈现一个 HTML 文件。

# 5.

今天到此为止，下次再见，祝你愉快。

我们的网站— [我在阅读](http://www.ihatereading.in)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***