# 5 个我多年来在开发中每天都在使用的便捷工具

> 原文：<https://javascript.plainenglish.io/5-handy-tools-that-i-have-used-daily-for-years-in-development-f5ab331467f?source=collection_archive---------13----------------------->

## 简单、实惠的工具，让您的生活更轻松！

![](img/f582ca21324ab6b073c963ff14f17858.png)

Photo by [Dan Cristian Pădureț](https://unsplash.com/@dancristianpaduret?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我看来，这些是少数几个有利于亚马逊的工具，我多年来每天都在使用它们。这些都是简单的工具，大多数情况下都是可以负担得起的，并且可以让您的生活更轻松，尤其是如果您不习惯部署的话。

# 1.亚马逊 EC2 —弹性计算云

这或多或少相当于亚马逊的副总裁。与更“经典”的 VPS 的区别在于有许多不同的定价和可能的配置。

请注意，您需要为每次使用付费，因此如果您停止实例，它将不再需要任何费用。如果你正在寻找一种更经典的 VPS 体验，我认为 AWS Lightsail 就是这样的。

# 2.亚马逊 S3-单一静态存储

顾名思义，亚马逊 S3 是一个静态文件存储系统(上传、下载但不执行)。例如，基本的使用允许存储应用程序的资源(图像、视频、JSON、XML ),并能够通过 S3 生成的 URL 请求它们。

但是最有趣的特性之一是可以使用“桶”作为静态网站主机(或者 web 应用程序的前端)。

只需上传您的文件，激活虚拟主机，瞧，您可以使用提供的 URL 访问您的网站！

# 3.亚马逊云锋

Cloudfront 是一个亚马逊风格的 CDN:只需输入 URL(或 bucket ),它必须从这个 URL 传送文件，一些可选的配置就可以了。

您可以选择在更新过程中使哪些文件路径无效，也可以让部署脚本为您完成这项工作。

Cloudfront 的真正资产是为 CDN 分配一个或多个域名的可能性，将 HTTP 请求重定向到 HTTPS，尤其是，由于 Amazon ACM 服务，可以简单免费地激活 SSL。

# 4.亚马逊证书管理器

该服务允许您生成一个免费的 SSL 证书(将您的域切换到 HTTPS)，只需在您的 DNS 配置中添加一行即可

证书验证在不到 2 分钟的时间内完成，如果你通过亚马逊的 DNS 服务器，只需一次点击，一切都是自动化的！

# 5.53 号公路

这是亚马逊的 DNS 配置服务。有两种方法可以使用它:

*   您可以将亚马逊提供的域名服务器分配给另一家注册服务商为您保留的域名
*   您可以直接从 Route53 预订域名

然后您的配置将像任何 DNS 管理器一样完成！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*