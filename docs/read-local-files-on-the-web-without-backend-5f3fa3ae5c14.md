# 使用 JavaScript 读取本地文件，无需后端

> 原文：<https://javascript.plainenglish.io/read-local-files-on-the-web-without-backend-5f3fa3ae5c14?source=collection_archive---------4----------------------->

## 使用纯 JS |不需要库

![](img/fcb51f42b05bda77ab740764c4323268.png)

Photo by [Mike van den Bos](https://unsplash.com/@mike_van_den_bos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这篇短文展示了一种简单的方法，使用纯 JS 与用户本地文件进行交互，而不需要通过网络传输数据。这种方法在大多数 chromium 浏览器中都可以使用，如 Google Chrome、MS Edge 等。

## 示例 1:读取文件及其元数据

以下示例使用简单的 HTML 输入从用户设备读取文件，并在浏览器控制台中打印出文件元数据。

## 示例 2:将文本文件作为字符串(或 JSON)读取

此示例包括一个解码 base 64 的函数和一个读取文件时要侦听的读取器事件。文件加载后，文本结果在目标 HTML 中作为字符串输出。

如果你的文件是 **JSON** 、 **XML** 等等，你可以包含一个解析函数。

[js dild](https://jsfiddle.net/JoeTS/qa372n56/7/)上的实例:

## 示例 3:读取图像文件

本示例将 HTML 页面上的图像源更新为用户上传的文件。

您可以包含示例 1 中的元数据读取器来检查上传的文件是否是图像。

[JSFiddle](https://jsfiddle.net/JoeTS/fn39xo5w/17/) 上的实例:

我希望你喜欢这篇文章，并发现它对你的日常工作或项目有用。

[](https://medium.com/@joets/membership) [## 通过我的推荐链接加入 Medium-Joe t . Santhanavanich

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@joets/membership) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***