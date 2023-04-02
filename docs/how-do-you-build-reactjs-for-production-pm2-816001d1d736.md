# 如何利用 PM2 建立生产反应

> 原文：<https://javascript.plainenglish.io/how-do-you-build-reactjs-for-production-pm2-816001d1d736?source=collection_archive---------1----------------------->

## 通过将 React 应用程序托管为静态构建，提高基本性能并减少加载时间。

![](img/8933e4fa3854e49902a096a7f2866351.png)

Reactjs with PM2

# 按照以下步骤操作:

## 1.创建一个反应应用程序(如果已经创建了一个项目，则忽略第一个命令)

```
npx create-react-app react-app && cd react-app
```

## 2.打开“反应”项目并运行命令:

```
npm run build
```

这将在您的项目中创建版本/文件夹。

## 3.现在安装 PM2 工具:它有助于在后台运行 react.js 应用程序。

```
sudo npm install -g pm2
```

## 4.在生成文件夹下创建一个名为 app.config.json 的新文件，并添加以下代码片段。

```
{
  apps : [
    {
      name      : "react-app",
      script    : "npx",
      interpreter: "none",
      args: "serve -s build -p 3000"
    }
  ]
}
```

> 现在我们已经准备好了，您可以根据需要从代码片段中更改 React.js 端口号(3000)和应用程序的名称(reactor-app)。

## 5.运行以下 pm2 命令，该命令将在您的本地或云实例(即 AWS EC2)上启动应用程序。

```
pm2 start app.config.json && pm2 list
```

> 该命令将启动应用程序，并显示 pm2 运行进程列表。

![](img/71e04616817c7f1e24cda7608d6054b6.png)

> **注意:**如果你喜欢这篇文章或者你想在 **AWS S3 桶**上发布另一篇关于托管 Action 应用的文章，请在评论中告诉我！

**遵循** **为** **的内容！**

[](/how-to-handle-undefined-null-and-empty-in-one-statement-javascr-44edbb045744) [## 如何在一条语句中处理未定义、空值和空值:JavaScript

### 在一条语句中处理未定义的、空的和空的条件:JavaScript

javascript.plainenglish.io](/how-to-handle-undefined-null-and-empty-in-one-statement-javascr-44edbb045744) 

*多内容于* [***中。***](https://plainenglish.io/) **[***报名参加我们的免费周报***](http://newsletter.plainenglish.io/) *。在* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*以及*[**T52**](https://discord.gg/GtDtUAvyhW)*上追随我们。****