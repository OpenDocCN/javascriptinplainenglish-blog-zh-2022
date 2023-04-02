# 使用 react-i18next 将本地化集成到 React 应用程序中

> 原文：<https://javascript.plainenglish.io/incorporate-localization-into-your-react-app-with-react-i18next-cc55bbdb0d50?source=collection_archive---------15----------------------->

![](img/84c9abd32966e570effa2b1bb8468cd3.png)

本地化可以让你的应用成功或失败，这取决于你想要的客户群。

准备好本地化的基础设施对于正确处理非常重要。

React 的国际化提供者有很多，但我最喜欢的是 [react-i18next](https://react.i18next.com/) 。

他们有很好的文档、简单的设置和使用最新 React 特性的工具，比如钩子，使开发人员能够快速上手并运行。

我想回顾一下我的 react-i18next 的简单实现，并强调一些让一切正常工作所需的核心特性。

我的例子将演示如何使用从 CDN 中提取的语言文件来设置本地化。

**安装**

我们需要做的第一件事是安装所有的软件包。

```
npm install react-i18next i18next i18next-browser-languagedetector i18next-http-backendor yarn add react-i18next i18next i18next-browser-languagedetector i18next-http-backend
```

**配置**

接下来，创建一个在应用程序启动时加载的配置文件。我将我的文件放在 src 文件夹的根目录下的一个名为 i18n.ts 的文件中

**配置高亮显示**

```
import LanguageDetector from “i18next-browser-languagedetector”
```

这个包用于从用户的浏览器中获取语言。有很多地方可以找到它。要获得完整的列表，我建议阅读他们的文件:[https://github.com/i18next/i18next-browser-languageDetector](https://github.com/i18next/i18next-browser-languageDetector)

```
import Backend from "i18next-http-backend"
```

这个包使您能够从 CDN 请求文件，并将它们合并到 i18next 生态系统中。[https://github.com/i18next/i18next-http-backend](https://github.com/i18next/i18next-http-backend)

```
const backendOpts = {  loadPath: "https://{bucket-name}.s3.amazonaws.com/localization/{{lng}}/{{ns}}.json",  crossDomain: true,}
```

这是我用来请求翻译文件的配置 URL 方案。你的可能看起来不一样。下面的 init 对象中设置了{{lng}}和{{ns}}变量，以供参考。

剩下的都是默认值，可以在这里找到:[https://react.i18next.com/latest/i18next-instance](https://react.i18next.com/latest/i18next-instance)

接下来，将配置导入到应用程序的根目录中

**用途**

下面是 translation.json 文件的一个基本示例:

下面是如何在功能组件中使用这些翻译:

react-i18next 提供了一个 [useTranslation hook](https://react.i18next.com/latest/usetranslation-hook) 作为将翻译拉入组件的最简单方式。

希望这能让您了解向 React 应用程序添加本地化是多么简单。这远不像过去那样是一项艰巨的任务。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*