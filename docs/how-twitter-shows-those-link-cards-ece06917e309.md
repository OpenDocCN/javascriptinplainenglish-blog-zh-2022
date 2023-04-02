# Twitter 如何展示这些链接卡

> 原文：<https://javascript.plainenglish.io/how-twitter-shows-those-link-cards-ece06917e309?source=collection_archive---------11----------------------->

## 以下是 Twitter 如何在每条推文中显示这些链接卡

![](img/da1c7e126b990b3d9a440042386ca1b0.png)

Twitter cards for our website

## 故事是如何开始的？

我想知道每当用户输入链接或粘贴 URL 时，Twitter 是如何创建这些卡片的。对于我们的网站，我们花了很多时间来通过 Twitter 卡验证测试案例。

## 为什么是元数据，什么是元数据？

所有的逻辑都与每个网页本身的元标签有关。meta 标签非常重要，它不仅可以帮助用户从域名/URL 获取你的网站数据，而且元数据还可以给谷歌爬虫提供更好的搜索引擎排名。

Google crawler 遍历网页并获取网站信息，如标题、描述、图像和标签，以向用户提供准确的搜索结果。

用最简单的方式理解逻辑，如果谷歌可以很容易地阅读你网站上的所有页面和它们相应的数据，它就可以更好地推荐给用户。

## Twitter 如何创建验证卡

twitter 使用了相同的概念，一旦 URL 被粘贴到文本框中，Twitter 就会运行验证器 API 来获取相应的链接元数据。

元数据由网站基本信息组成，如标题、横幅图像、描述、标签等。利用这些信息，Twitter 可以在几秒钟内生成这些酷卡。

虽然 twitter 使用自己的元标签，所以如果没有提供 twitter 将能够显示你的网站卡。这个概念耗费了我大量的时间，所以当你为 Twitter 卡片添加元数据时，一定要阅读添加 Twitter meta 标签的文档。

## 检测您的网站元数据

我开发了一个 API 来检测你自己的自定义域名的元数据， [**这里是检查你的网站元数据的链接**](https://ihatereading.in/projects/metascanner) 。

如果你的元数据不可用，那么确保你把它们完全添加到你的网站上。

这个想法很简单，任何人都可以创建自己的定制元数据获取 API 或模块。事实上，使用内部的元数据获取 API，我们也可以在自己的网站上开发卡片，就像 Twitter 一样。

## 我做得怎么样？

*   我开发了一个内部元数据获取 API。
*   一旦 URL 和链接被添加到任何日志中，我们就使用 API 从相应的链接中获取元数据
*   最后，我们只需要使用来自元数据 API 的响应来呈现卡片。

## 如何创建元数据抓取 API？

*   创建需要参数中的 URL 的元数据提取路由
*   使用这个 npm 模块，帮助服务器从参数中传递的每个链接获取元数据。
*   或者你可以使用木偶师抓取相应的网站并获取元数据，这不是火箭科学。
*   在路由响应中返回所需的元数据。

## 结论

这整个逻辑可能看起来很容易，但我花了很多时间和阅读和研究的核心逻辑运行的引擎盖下。

在研究 twitter 如何展示卡片时，我复制粘贴了文本框中的链接，同时查看了 chrome 网络标签。一旦 URL 被添加到 tweet textbox，twitter 就会立即运行 API，从相应的链接中获取元数据。

今天就到这里，希望你喜欢这个概念，深入理解这个概念有时很有趣也很令人沮丧。这些概念不是由很多新开发人员发布在互联网上的。对开发者来说是一个有趣又有见识的小项目，可以试试。

今天就到这里，下次再见，祝你愉快。

```
You can read all my articles at without paying on [**iHateReading**](http://ihatereading.in)
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*