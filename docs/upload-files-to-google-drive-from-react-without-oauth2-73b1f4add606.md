# 从 React 上传文件到 Google Drive，无需 OAuth2

> 原文：<https://javascript.plainenglish.io/upload-files-to-google-drive-from-react-without-oauth2-73b1f4add606?source=collection_archive---------1----------------------->

## 在 Node.js 和 Multer 的帮助下，没有 OAuth2！

![](img/4085646e118566eef20cc289a6a606ee.png)

Photo by [Alesia Kazantceva](https://unsplash.com/@alesiaskaz?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

使用 Google 服务需要 OAuth2 认证，这实现起来有点复杂，如果你只是想实现一个简单的功能，可能不值得这么麻烦。

今天我们将学习如何使用服务帐户将文件上传到 google drive。它将允许我们避免实现 OAuth2 身份验证。

## 视频格式:

如果你喜欢视频格式，这里是这样的:

如果没有，我们继续。

# 先决条件

1.  首先要做的是创建一个服务帐户并获取`key.json`文件。从您的谷歌云控制台
2.  然后，您需要在您的控制台上启用 google drive API
3.  在下载的 key.json 文件中，您会看到一个`client_email`字段。复制该值。
4.  转到您想要通过 API 访问的 google drive，并与该电子邮件帐户共享该文件夹/文件。

最后一步很重要，因为它将允许我们避免实现 OAuth2 身份验证。

# 准备前端

创建新的 React 应用程序。

前端代码非常容易。我们只需要一个文件选择器从本地机器上选择一个文件，并将其发送到 Node.js 服务器。

GoogleDriveFileUploader.tsx

这是一个简单的组件，允许我们从本地存储中选择一个文件，并调用我们接下来要开发的 API。

# 准备后端

让我们首先通过安装一些依赖项来初始化项目。

```
yarn add googleapis express cors multer
```

这里的`multer`是一个用于`express`应用程序的特殊中间件，帮助文件上传

`googleapis`是我们与谷歌云 API 交互的方式。

我们先来回顾一下我们要做的事情。

## 配置乘法器

1.  我们将使用`multer`配置我们的磁盘存储。这将允许我们将收到的文件存储在指定的文件夹中。

## 验证我们的应用程序

然后，我们将使用 key.json 文件创建并授权我们的应用程序代码。

然后创建我们的函数来处理文件上传特性。

注意在`fileMetadata`字段中有一个**父**数组。这是我们要将文件上传到的 google drive 文件夹的 id。

在我们将文件上传到 google drive 后，我们也想删除该文件。让我们为此创建另一个函数。

```
const deleteFile = (filePath) => {
  fs.unlink(filePath, () => {
    console.log("file deleted");
  });
};
```

最后，让我们得到我们的端点，并一起使用所有这些。

# 获取文件列表

在前面的步骤中，我们注意到我们使用了一个 ID 来指定我们想要将文件上传到的文件夹。我们可以使用下面的函数来列出与这个特定服务帐户共享的可用文件和文件夹。

```
const response = await drive.files.list(params);
```

从响应中，我们将得到一个可以找到文件 id 的列表。

# 上传文件而不存储它

上述解决方案非常有效。直到得到不能在磁盘上存储文件的要求。

例如，当您在 docker 中运行应用程序而没有 root 权限时，您必须授予非 root 用户权限。否则，您会得到一个错误，因为该特定用户无法将文件存储在存储器中。

为了解决这个问题，Multer 为我们提供了另一个选择。我们用 `multer’s` `memorystorage`就可以了。

它会将文件存储在应用程序内存中。如果文件大小不是超级疯狂的话，应该不成问题。只需在这里进行配置。

你可以走了！

今天到此为止。希望你学到了新东西。

祝您愉快！

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) **或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*