# 从 React 上传文件到 Google 云存储

> 原文：<https://javascript.plainenglish.io/upload-files-to-google-cloud-storage-from-react-cf839d7361a5?source=collection_archive---------2----------------------->

## 关于如何使用 Node.js 和 Multer 将文件从 React 上传到 Google 云存储的教程

![](img/5912b5f1dad7086b1f7de82124e56997.png)

Photo by [Aideal Hwa](https://unsplash.com/@aideal?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

今天，我们将了解如何使用 Node.js 后端从 React 前端向 Google 云存储上传文件。

# 第一步:做前端

前端代码非常容易。我们只需要一个文件选择器从本地机器上选择一个文件，并将其发送到 Node.js 服务器。

GoogleStorageFileUploader.tsx

# 准备云存储:

转到您的 Google Cloud 控制台，创建一个有权将文件上传到 Google 云存储的服务帐户。

然后下载该服务帐户的密钥文件，并将其存储在一个安全的地方。

然后在你的云控制台中选择云存储，创建一个存储桶。

为了避免这篇文章太长，我们没有在这里展示这一部分。

# 准备后端

让我们首先通过安装一些依赖项来初始化项目。

```
yarn add @google-cloud/storage express cors multer
```

这里 multer 是一个特殊的 Express 中间件，帮助文件上传。

`@google-cloud/storage`是我们上传文件到谷歌云存储的客户端。

然后使用以下代码创建我们的服务器:

1.  这里我们正在创建我们的 Express 应用程序。
2.  然后我们创建一个 multer 实例。
3.  然后通过提供云存储客户端的路径来配置我们的云存储客户端

```
import { Storage } from "@google-cloud/storage";
import express from "express";
import cors from "cors";
import { format } from "util";
import Multer from "multer";
const app = express();
const port = 5000;const multer = Multer({
  storage: Multer.memoryStorage(),
  limits: {
    fileSize: 5 * 1024 * 1024, // no larger than 5mb, you can change as needed.
  },
});app.use(cors());const cloudStorage = new Storage({
  keyFilename: `${__dirname}/service_account_key.json`,
  projectId: "PROJECT_ID",
});
const bucketName = "YOUR_BUCKET_NAME";const bucket = cloudStorage.bucket(bucketName);app.post("/upload-file-to-cloud-storage", multer.single("file"), function (req, res, next) {
  if (!req.file) {
    res.status(400).send("No file uploaded.");
    return;
  } const blob = bucket.file(req.file.originalname);
  const blobStream = blob.createWriteStream(); blobStream.on("error", (err) => {
    next(err);
  }); blobStream.on("finish", () => {
    // The public URL can be used to directly access the file via HTTP.
    const publicUrl = format(`https://storage.googleapis.com/${bucket.name}/${blob.name}`); res.status(200).json({ publicUrl });
  }); blobStream.end(req.file.buffer);
  console.log(req.file);
});app.listen(port, () => {
  console.log(`listening at http://localhost:${port}`);
});
```

然后使用以下命令启动服务器:

```
node index.js
```

保持服务器运行，并尝试使用我们的 React 前端上传文件。

# 下载文件

您还可以使用同一个客户端库从云存储中下载文件。使用以下函数生成一个签名的下载 URL，使您可以安全地访问该文件。

```
app.get("/get-url", (req, res) => {
  const file = bucket.file("FILE_NAME_IN_THE_BUCKET");
  const config: any = {
    action: "read", // giving read permission here
    expires: "03-17-2025", // specifying the expiry date
  };
  file.getSignedUrl(config, (err, url) => {
    res.status(200).json({ url });
  });
});
```

# 列出文件

要从云存储中获取文件列表，可以使用以下代码:

```
app.get("/get-files-list", async (req, res) => {
  const options = {
    prefix: "audio", // or anything you want!
  };
  const [files] = await bucket.getFiles(options);
  res.status(200).json({ files });
});
```

所以这是一个超级短的教程，向你展示如何上传文件到谷歌云存储。希望你今天学到了新东西！

祝您愉快！

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) **或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**

[](/upload-files-to-google-drive-from-react-without-oauth2-73b1f4add606) [## 从 React 上传文件到 Google Drive，无需 OAuth2

### 在 Node.js 和 Multer 的帮助下，没有 OAuth2！

javascript.plainenglish.io](/upload-files-to-google-drive-from-react-without-oauth2-73b1f4add606) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*