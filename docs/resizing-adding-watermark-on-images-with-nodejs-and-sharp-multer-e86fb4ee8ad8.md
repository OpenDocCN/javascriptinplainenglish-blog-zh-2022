# 用 Node.js 和 Sharp-Multer 在图像上调整大小和添加水印

> 原文：<https://javascript.plainenglish.io/resizing-adding-watermark-on-images-with-nodejs-and-sharp-multer-e86fb4ee8ad8?source=collection_archive---------9----------------------->

![](img/28032ebfb284daef690a14a06b8a08ee.png)

# 动机:

每当我们开始上传图片时，调整大小是第一位的，通常我们还需要添加水印。

在上一篇[文章](https://dev.to/ranjan/simple-node-js-resize-image-before-upload-using-sharp-multer-p8c)中，我们学习了如何用[锐化工具](https://www.npmjs.com/package/sharp-multer)设置图像的基本尺寸调整和优化。在这里，我们将添加先进的调整大小和添加水印到所有上传的图像。

# 先决条件:

请在此阅读本系列的[第 1 部分](https://dev.to/ranjan/simple-node-js-resize-image-before-upload-using-sharp-multer-p8c)。

# 设置和配置:

在上一部分中，我们设置了一个简单的 Node.js 应用程序，这些文件包含以下代码:

# Server.js

```
const express = require("express");
const path = require("path");
const multer = require("multer");
const SharpMulter = require("sharp-multer");
const app = express();const storage = SharpMulter({
  destination: (req, file, callback) => callback(null, "images"),
  imageOptions: {
    fileFormat: "png",
    quality: 80,
    resize: { width: 500, height: 500 },
  }
});
const upload = multer({ storage });app.post("/upload", upload.single("avatar"), async (req, res) => {
  console.log(req.file);
  return res.json("File Uploaded Successfully!");
});
app.get("/", function (req, res) {
  res.sendFile(path.join(__dirname, "/index.html"));
});app.listen(3000, () => {
  console.log(`Server is running on port ${3000}`);
});
```

# index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    <title>File Upload</title>
</head>
<body>
    <div class="container">
        <h1>File Upload</h1>
<!--Create a form to send the file to a route  "upload"-->
<!--Set the request method to POST-->
<!--Set the encytype to "multipart/form-data" in order to send files and not just text-->
        <form action="/upload" method="POST" enctype="multipart/form-data">
            <div class="file-field input-field">
              <div class="btn grey">
                <input type="file" name="avatar">
              </div>
            </div>
            <button class="btn" type="submit">Submit</button>
          </form>
    </div>
</body>
</html>
```

我们已经有了基本的尺寸调整和优化，但是现在有了`sharp-multer 0.2.1`，我们有了一些高级的尺寸调整选项。我们现在可以定义图像使用哪种大小调整模式。

# 尺寸模式

> *resize.resizeMode*

*   `cover`:(默认)保留纵横比，通过裁剪/剪裁来确保图像覆盖提供的两个尺寸。
*   `contain`:保留纵横比，包含在两个提供的尺寸中，必要时使用“信箱模式”。
*   `fill`:忽略输入的长宽比，拉伸到两个提供的尺寸。*即图像将被拉伸以匹配所提供的尺寸*
*   `inside`:保持纵横比，在保证图像尺寸小于或等于指定尺寸的情况下，尽可能放大图像。*即宽度将固定为您提供的最大值，而高度将根据纵横比*调整为比提供的值更低的值。
*   `outside`:保持宽高比，在保证图像尺寸大于或等于指定尺寸的情况下，尽可能缩小图像尺寸。*即高度将固定为您提供的值，宽度将根据长宽比调整为比提供的值更高的值。*

要使用它，我们需要在 imageOptions resize 对象中提供 resizeMode 键，例如:

```
imageOptions: {
    fileFormat: "png",
    quality: 80,
    resize: { width: 500, height: 500, resizeMode: "outside" },
  }
```

# 添加水印

使用新的 sharp-multer，添加水印非常容易。我们可以只提供输入图像路径和我们想要放置水印的位置。
目前我们可以在这些位置放置水印:`"center","top-left","top-right","bottom-left","bottom-right"`。因此，为了添加水印，我们的存储配置将如下所示:

```
const storage = SharpMulter({
  destination: (req, file, callback) => callback(null, "images"),
  imageOptions: {
    fileFormat: "png",
    quality: 80,
    resize: { width: 500, height: 500, resizeMode: "outside" },
  },
  watermarkOptions: {
    input: "./images/logo.png", // watermark image location
    location: "top-right",
  },
});
```

你可以在这个[回购](https://github.com/ranjandsingh/image-upload-resize-test.git)里找到完整的代码。试试看，玩得开心。干杯！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****