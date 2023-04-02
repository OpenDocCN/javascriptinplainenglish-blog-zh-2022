# 使用 Nodemailer 编辑用 HTML、CSS 和 Handlebars 创建的自定义动态电子邮件模板

> 原文：<https://javascript.plainenglish.io/nodemailer-custom-dynamic-email-templates-with-html-css-and-handlebars-9b72283575d9?source=collection_archive---------2----------------------->

## 关于如何使用 Nodemailer 来编辑已经用 HTML 和 CSS 创建的自定义动态电子邮件模板的教程。

![](img/6a4d4ac140b5ec8cf0b758750302fd18.png)

Photo by [Claudio Schwarz](https://unsplash.com/@purzlbaum?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Nodemailer 是 Node.js 应用程序的最佳邮件库之一。我使用 Nodemailer 已经很久了。将 Nodemailer 添加到您现有的应用程序中非常容易。

Nodemailer 是 Node.js 中使用最多的邮件库，它成为了大多数 Node.js 用户发送电子邮件的解决方案。

今天我将解释如何将 Nodemailer 用于已经用 HTML 和 CSS 创建的定制 HTML 模板。我将在本教程中介绍的另一个主题是编辑这些电子邮件中的动态区域。

假设有一个用户注册了您的应用程序，您希望向该用户发送一封电子邮件，并在邮件中写上他们的姓名。您将在本教程中学习如何做到这一点。

如果您以前从未使用过 Nodemailer，我建议您阅读另一篇关于 Nodemailer 的文章，对它有一个基本的了解。

[](/how-to-send-email-with-nodemailer-with-examples-356b348dccac) [## 如何用 Nodemailer 发送电子邮件并举例说明

### 如何使用 Nodemailer 通过 Node.js 发送电子邮件:TypeScript 中带有示例代码的教程。

javascript.plainenglish.io](/how-to-send-email-with-nodemailer-with-examples-356b348dccac) 

# 我们开始吧

首先，如果你有一个现有的应用程序，或者如果你刚刚开始一个新的服务器，我们需要安装我们想要使用的软件包。

因此，在这里，您可以使用 npm 或 yarn 进行安装。

**如何安装节点邮件器**

```
npm install nodemaileryarn add nodemailer
```

将 Nodemailer 安装到您的应用程序后，您就可以立即发送电子邮件了！

## 发送电子邮件

以下是发送电子邮件的要点示例:

正如您在这里看到的，HTML 部分只包含:

```
html: "<strong>Hello world?</strong>"
```

但是如果我们想要发送已经创建并实际存储为一个`HTML`文件的 HTML 消息呢？

## 创建带手柄的动态 HTML 模板

首先，我们需要用 Node.js 文件系统读取该文件。如果您还没有创建一个`HTML`文件，您可以创建一个用于测试的如下文件。

```
<!DOCTYPE html>
<html>
<body>

<h1>My First Heading</h1><p>My first paragraph.</p><p>Hello world, {{username}} </p></body>
</html>
```

正如你在那个例子中注意到的，我们也在 HTML 文件中添加了一些变量`{{username}}`是我们在发送电子邮件时可以动态改变的变量。

## 安装把手和编辑 HTML 模板

在继续之前，我们需要将`handlebars`包安装到我们的应用程序中，以动态编辑用户名变量。
更多信息:

[](https://handlebarsjs.com/) [## 把手

### 类固醇上的最小模板开始→手柄提供必要的力量让你建立语义…

handlebarsjs.com](https://handlebarsjs.com/) 

```
npm install handlebarsyarn add handlebars 
```

成功完成车把安装后，我们可以在 Node.js 中编译 HTML 代码，并根据需要更改变量。

```
const filePath = path.join(__dirname, '../emails/template.html');
const source = fs.readFileSync(filePath, 'utf-8').toString();
const template = handlebars.compile(source);
const replacements = {
    username: "Darth Vader"
};
const htmlToSend = template(replacements);
```

## 发送电子邮件模板

在成功编译和替换我们的 HTML 模板后，它就可以发送了。我们可以用`htmlToSend`替换 HTML 值，而不是在`transporter.sendMail`函数中传递静态 HTML 文本。

*如果你觉得这篇文章很有帮助，你* [***可以通过使用我的推荐链接注册一个***](https://medium.com/@melihyumak) **[***中级会员来访问类似的***](https://melihyumak.medium.com/membership) *。***

***跟我上*** [**推特**](https://twitter.com/hadnazzar)

![](img/e09adde9fd734db2f987c8df72839da8.png)

Subscribe for more on [Youtube](https://www.youtube.com/c/TechnologyandSoftware?sub_confirmation=1)

# 编码快乐！

梅利赫

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。**