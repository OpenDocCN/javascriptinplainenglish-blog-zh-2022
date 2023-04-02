# 轻松找到并删除旧的和沉重的“节点模块”文件夹✨

> 原文：<https://javascript.plainenglish.io/easily-find-and-remove-old-and-heavy-node-modules-folders-fa0e10f57029?source=collection_archive---------11----------------------->

## 使用此库可以轻松找到并删除大量的“node_modules”文件夹。

![](img/82d3ddbe1f4833fa05d124336ca5d797.png)

node_modules are really heavy

我是一名 UI 开发人员，我喜欢通过启动小项目来尝试新事物。我最终在你的电脑上有许多 UI 项目。它们每个都有一个 node_modules 文件夹，即使项目本身很小，它占用的空间也很大。

在几个项目之后，我经常会耗尽系统中的空间。

虽然我可以去每个项目并单独删除 node_modules，但这是一项单调乏味的任务。

我最近偶然发现了这个图书馆，它是我的救命稻草。

[](https://github.com/voidcosmos/npkill) [## GitHub - voidcosmos/npkill:列出系统中的所有 node_modules 目录，以及空间……

### 列出系统中的所有 node_modules 目录，以及它们占用的空间。然后你可以选择你…

github.com](https://github.com/voidcosmos/npkill) 

现在有了 [npkill](https://github.com/voidcosmos/npkill) ，我需要做的就是运行:

```
npx npkill
```

它将列出所有 node_modules 文件夹。现在，我可以使用键盘在目录间导航，并按空格键删除它。

> 注意:即使我们可以进入每个目录，然后并行删除，根据硬盘的性能，这可能需要更长的时间。如果你和我一样用的是比较慢的，一次删除一个。

非常感谢这个项目的所有贡献者。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/)***[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。****