# Vite 4 Beta 出来了！

> 原文：<https://javascript.plainenglish.io/vite-4-beta-is-out-5f2233c6dbd6?source=collection_archive---------7----------------------->

![](img/8c3c79854eee998cbe2381fee5272455.png)

# 介绍

如果你是前端开发人员，或者对前端开发感兴趣，你大概会听说过 Vite。

Vite 是一个前端构建工具，具有即时服务器启动和丰富的功能。Vite 刚刚宣布了 Vite 4 Beta，我将总结一下它的变化

# 累计 3

Vite 现在使用的是 [Rollup 3](https://github.com/vitejs/vite/issues/9870) ，它允许我们简化 Vite 的内部资产处理，并且有很多改进。

Rollup 3 提供了更多的功能和修复的 bug，你可以在这里查看详情

## 开发期间使用 SWC 的新 React 插件

SWC(或称 Speedy Web Compiler)是一个可扩展的基于 Rust 的平台，用于下一代快速开发工具。它被 Next.js、Parcel 和 Deno 等工具以及 Vercel、字节跳动、腾讯、Shopify 等公司使用。

在 Vite 4 中，有两个插件可用于 React 项目，具有不同的权衡:

*   @vitejs/plugin-react
*   @vitejs/plugin-react-swc

Vite 认为这两种方法在这一点上都值得支持，并将在未来继续探索对这两种插件的改进。

## 将 CSS 作为字符串导入

在 Vite 3 中，导入默认导出的`.css`文件可能会导致 CSS 的双重加载。

```
import cssString from './global.css';
```

因为`.css`文件将被发出，但是 CSS 字符串也可能被应用程序代码使用，例如，被框架运行时注入。从 Vite 4 开始，`.css`默认导出[已经被弃用](https://github.com/vitejs/vite/issues/11094)。在这种情况下，需要使用`?inline`查询后缀修饰符，因为它不会发出导入的`.css`样式。

```
import stuff from './global.css?inline'
```

# 其他东西

在 Vite 4 中还有许多其他的东西:

*   默认支持`safari14`
*   支持环境文件中的多行值
*   将@types/node 更新到版本 18
*   支持修补程序包

还有很多很多其他的事情，比如漏洞修复、改进和优化，你可以在这里查看[变更日志](https://github.com/vitejs/vite/blob/main/packages/vite/CHANGELOG.md#vitejsplugin-react-swc-new)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****想看看你的软件启动规模*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。**