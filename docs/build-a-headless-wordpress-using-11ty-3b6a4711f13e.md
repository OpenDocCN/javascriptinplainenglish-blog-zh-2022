# 使用 11ty 构建一个无头 WordPress

> 原文：<https://javascript.plainenglish.io/build-a-headless-wordpress-using-11ty-3b6a4711f13e?source=collection_archive---------17----------------------->

## WordPress 是世界上最流行的内容管理系统之一。然而，也有不利的一面，像 11ty 这样的 SSG 可以帮助打开可能性。

![](img/94514f0ae7f5fc8e40a423e72669e357.png)

11ty is a simple static site generator

WordPress 被广泛认为是世界上最流行的内容管理系统之一。

事实上，截至 2021 年末， [WordPress 为世界上 100 万个顶级网站中的 35%提供支持](https://gracethemes.com/wordpress-is-still-the-most-popular-cms-choice-top-trends-in-2020-and-predictions-for-2021/)。太了不起了！

## 为什么这么受欢迎？

首先，它是免费下载和使用的。但是，如果你想定制它，WordPress 确实会对它的一些模板和插件收取费用。尤其是一些最有用的。

除了免费，WordPress 的无处不在意味着如果你是互联网上的内容创作者，你可能以前用过它。

如果您还没有，那也没关系，因为它非常用户友好。此外，它足够灵活，不仅可以像博客一样发挥作用，还可以用于许多不同的项目。

## 使用 WordPress 的缺点

尽管它非常受欢迎，但使用 WordPress 也有一些严重的缺点。

一个是安全性，因为它太受欢迎了。黑客用的逻辑是，如果流行，弄清楚如何黑进去更有意义。然后，一旦发现如何，这个过程可以重复。

另一个缺点是 WordPress 网站的下载速度较慢。这意味着观众在等待网站加载，可能会变得不感兴趣并离开。他们使用多余的代码和沉重的主题肯定会损害他们网站的速度。

最后，插件的必要性是第三个缺点。一次使用许多插件会导致加载时间缓慢。最重要的是，许多重要的插件只有通过支付年费才能获得。这意味着你的“免费”网站一年的运营时间要长得多。

## 解决方案

幸运的是，有一种方法可以解决我们上面提到的所有问题。

它被称为“无头 WordPress”

Headless 可能听起来很吓人——就像《行尸走肉》中的东西——但它只是指使用 WordPress 来管理内容，并使用不同的框架来显示内容。

在这个例子中，我们将使用 [Eleventy (11ty)](https://www.11ty.dev/) ，一个他们自称的“更简单的静态站点生成器”。

![](img/55a6ac96a1c599ce7bb1e613506fa9b2.png)

## 是什么让 Eleventy 如此伟大？

它有多个不同的模板和多种不同的 JavaScript 语言。当您使用微前端时，这无疑是一个优势，因为它们也可以使用最适合您的 JavaScript 语言。

11ty 还明确表示，他们的产品本身不是一个 JavaScript 框架，而是一个静态的站点生成器。SSG 最好的一个方面是它们在构建时被预先渲染，这意味着当访问者请求它们时，它们会以令人难以置信的速度加载。与 WordPress 及其缓慢的加载速度相比，这是一个重大的升级。

除了更快的加载时间，因为站点是用静态站点生成器预先呈现的，这也有助于站点的 SEO，因为搜索引擎可以找到呈现的数据。相比之下，单页应用程序(SPAs)的 WordPress 站点只发送回一个空白的 HTML 页面。

Eleventy 的另一个坚实的方面是他们拥有的模板。这意味着客户或开发人员不必从头开始。它让网站的建立和运行变得又快又简单。

更进一步，我们实际上已经使用了 11ty。Fathym 的 George Hatch 将 Eleventy 作为其网站的一部分，该网站利用了各种开源应用。

结果是易于使用的内容管理和一个具有电子商务功能的网站——由 Fathym 托管——由于 11ty 和我们的微前端，他能够在短短几分钟内[快速上线。](https://www.fathym.com/blog/articles/2022/february/2022-02-23-flashup-use-case-redwood-crystals)

今天就把你的 WordPress [网站转移到 fat hym](https://auth.fathym.com/fathymcloudprd.onmicrosoft.com/oauth2/v2.0/authorize?p=b2c_1_sign_up_sign_in&client_id=98f014f1-2547-4bcc-a583-3edc8f1190f2&redirect_uri=https%3A%2F%2Fwww.lowcodeunit.com%2F.oauth%2FB2C_1_SIGN_UP_SIGN_IN&response_type=id_token&scope=openid%20profile&response_mode=form_post&nonce=637789907534834707.OWNhMWZkZGMtODQ2NC00YTg0LWFjZWQtYjlkNzg0YTIzMDhkYTcxMzVkZmYtN2E2Mi00ZDRlLWIxODQtZjMxMjBkNWI2OTEx&state=CfDJ8C5COa2dn0dMrEVjdLxcXm-FCakeBxrXIOHa_lF_u0ckh9rvLFuKJ30MWBprExUQA_N5HmWWWPdxqWlni-KFqpg_jVjPahrQdGw79U0sMBN8dTvgrlAMeT9--L-7VgMBsZfFPAho9dcKUN1jO6lAaxL13PM1_vGer-vJc6tcpigRpNr5jcHtitGIKjexLmQqkIslp3MFKCKAi-5IiVd3JbpibPm4gbmDQpYtgstmG9SSlpjvEqJk_2AIqtMHkiojK3kE4WSc5mcYS3FQ3hiRqVQRPlL3jI7U3bUsqGYtLuoJr_St6mGBbHvGmB6M0MCeFn_G5LDsRzyHZhBWf9a1qo6dktz_kEcsAahYPLWjAI_2&x-client-SKU=ID_NETSTANDARD2_0&x-client-ver=6.11.1.0)上，用 Eleventy 免费试用。一旦你看到速度和用户体验的提高，我们有一种感觉，你会留下来。

这个题目到此为止。感谢您的阅读。

*原载于*[*https://www.fathym.com*](https://www.fathym.com/blog/articles/2022/march/2022-03-29-headless-wordpress-using-eleventy)*。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**