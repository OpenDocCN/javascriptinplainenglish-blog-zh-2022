# 如何使用 Next.js 将文件上传到 AWS S3

> 原文：<https://javascript.plainenglish.io/how-to-upload-a-file-to-aws-s3-using-next-js-b89482da7c64?source=collection_archive---------2----------------------->

## 将文件从客户端/浏览器内置的 Next.js 直接上传到 AWS S3 的分步指南。

![](img/6e6529b46ab52b8dbcf4e9a07890a840.png)

Photo by [Mike van den Bos](https://unsplash.com/@mike_van_den_bos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这篇小文章将一步一步地将文件从客户端/浏览器内置的 NextJS 上传到 AWS 的 S3。

Next.js 组件的代码如下所示

fileUpload.tsx

在这个组件定义中，我们有一个`input`字段，它设置上传文件的值。

然后，我们使用`useEffect`函数观察`file`字段状态的任何变化。从那里，我们调用我们的`uploadFile`函数，它利用了 NextJs 的 [API routes](https://nextjs.org/docs/api-routes/introduction) 。

对于 API 构建的这一部分，您需要安装`aws-sdk`和`axios`包

```
npm install --save aws-sdk axios
```

现在，在`/pages/api/s3`文件夹&中创建一个新文件，命名为`upload.ts`，并添加以下代码

upload.ts

这个 API 所做的就是从`NextApiRequest`主体接收文件名和类型，并使用它们获得一个 S3 `signedURL`。确保你已经用正确的`access key` & `access secret`初始化了 S3 对象

一旦有了签名的 URL，使用它从组件本身上传到 S3，如`line 17`上的`fileUpload.tsx`所示。

*   **演示现场**:[https://tools.meta-collective.co.uk/colorpicker](https://tools.meta-collective.co.uk/colorpicker)
*   **GitHub**:[https://github.com/metacollective9/canvasfun](https://github.com/metacollective9/canvasfun)

感谢您的阅读，如果您想支持我，那么请关注我，成为会员，帮助我们所有人在这个平台上成长和制作有用的内容。

[](https://medium.com/@metacollective/membership) [## 通过我的推荐链接加入媒体 Meta Collective

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@metacollective/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***