# 添加绝对导入的 4 个步骤

> 原文：<https://javascript.plainenglish.io/4-steps-to-add-absolute-import-56a0631c943?source=collection_archive---------6----------------------->

## 你真的用绝对导入来提高代码读写。

![](img/090804dde218fc619154d9fd0ce8cf88.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 介绍

在今天的故事中，我们将学习从绝对路径导入模块。我们将学习从根目录开始从绝对路径导入，而不是从现有路径导入包和组件。

## 第一步

在当前的 React 应用程序中安装 Next.js。我假设你有 Next.js 库，如果没有的话，去[他的链接下载你的第一个 Next.js 库](https://ihatereading.in/createrepo?framework=Next%20JS&repoId=-MgQlG5flVPCV7sJyRYh)。

## 第二步

在根目录下创建`jsconfig.json`文件，一旦创建了项目，就很容易在根目录下添加`jsconfig.json`文件。

## 第三步

将根路径作为值添加到配置文件中。只需在配置文件中添加以下代码。

```
{
 "compilerOptions": {
   "baseUrl": "."
  }
}
```

## 第四步

使用 baseUrl 作为起点开始导入组件。

# 结论

下次见，祝你愉快。

继续发展！！

我们的网站[我在读](https://www.ihatereading.in/)| |[Youtube](https://www.youtube.com/channel/UC6I-Tz6QwYbJpoIK7l0NtXA)| |[Twitter](https://twitter.com/treyvijay)。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***