# 如何为 Fetch 请求编写 TypeScript 模块

> 原文：<https://javascript.plainenglish.io/how-to-write-a-typescript-module-for-fetch-requests-deecc9742a63?source=collection_archive---------7----------------------->

## 编写模块化和可重用的 API 调用

![](img/f177f7de1aecf2691d36bbe2fd2fcfdf.png)

Photo by [Pathum Danthanarayana](https://unsplash.com/@pathum_danthanarayana?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/elegance?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

最近我一直在重构很多代码，从 JavaScript 到 TypeScript。在这样做的时候，我还试图使它更加模块化，并更清晰地注入依赖关系。我认为这是一种更优雅的设计模式…

因此，频繁地向一些不同的 API 发出大量的获取请求，我最终为此编写了非常相似的 TypeScript 模块。我发现这是一个非常有用的方法。我在网上见过很多这样做的方法，但我个人觉得这种方法更简单明了，所以我想在这里分享一下:

我喜欢这种方法的一点是，编写一堆调用相同 API 的方法变得非常容易，就像您在第 24–32 行看到的那样。

在其他地方以类似的模式重用这段代码也很容易，因为您在第 35 行非常清楚地注入了基本 URL 依赖。

最后但同样重要的是，我发现在编写测试时采用这种方法真的很有帮助。像这样用不同的方法在一个模块中非常清楚地定义所有的东西，使得模仿这个文件中的方法变得非常容易，而不需要做更多的全局或复杂的模仿。这使得测试变得更加有趣。

最后但并非最不重要的一点是，用这种方式保持一切异步非常容易，而且当您导入方法而不是编写和重复大量提取逻辑时，代码看起来更整洁。

例如，要使用`getPosts`方法，您可以只写:

```
import makeRequests from "./fetchutils/fetch";const results = await makeRequests.getPosts();console.log(results);
```

这就对了。简单的东西，但如果你像我一样最终重构一个大的旧 JavaScript 代码库，希望会有帮助。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***