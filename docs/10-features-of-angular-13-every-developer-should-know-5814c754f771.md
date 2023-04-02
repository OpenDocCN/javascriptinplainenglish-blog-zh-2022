# 每个开发人员都应该知道的 Angular 13 的 10 个特性

> 原文：<https://javascript.plainenglish.io/10-features-of-angular-13-every-developer-should-know-5814c754f771?source=collection_archive---------3----------------------->

## Angular 正在非常迅速地走向美好的未来

![](img/1c48e5cd9fff783031b85827638cfd86.png)

Photo by [bruce mars](https://unsplash.com/@brucemars?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

2021 年 11 月，谷歌的团队推出了 Angular 的另一个更新版本，即 v13。Angular 13 为开发社区带来了一些令人兴奋的功能。

Google 的核心开发团队总是说他们每个新版本的目标是找到切实可行的方法来改进 Angular。他们通过扩展基于 Ivy 的特性和优化，与优秀的 Angular 社区合作，并继续为开发团队和项目提供平稳、稳定的更新过程，在这个版本中实现了这一点。

如果你想知道 Angular 13 有什么新功能，这里有一个关键功能的快速概述。

## 1.视图引擎不再使用

![](img/5ee70866413780b22aa7d1086d739391.png)

Photo by [Erik Mclean](https://unsplash.com/@introspectivedsgn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Angular 的最新版本 Angular 13 不再支持古董视图引擎。使用视图引擎会导致维护成本，并增加 Angular 13 代码库的复杂性。为了避免这种麻烦，Angular 现在只支持 Ivy 作为视图引擎。

此更改的结果是，一些现有库将自动迁移到部分编译模式，并且一些以前传统视图引擎所需的元数据将被删除。此外，为了确保平稳过渡，所有内部工具都提前转换为 Ivy。

Ivy 现在可以相互独立地编译单个组件，这大大提高了性能。Angular 可以通过移除视图引擎来减少对 ngcc 的依赖。

## 2.角度包装格式(APF)的修改

![](img/9f6c61fcea58ed1b1566d39abe3addaf.png)

Photo by [Henry & Co.](https://unsplash.com/@hngstrm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

角度包格式(APF)指定了角度框架包以及视图引擎元数据的结构和格式。这是在 web 开发环境中打包每个第三方库的好方法。

新版本的倡导性政策框架包含一些重大变化。在 Angular 13 中，旧的输出格式(包括一些特定于视图引擎的元数据)已被弃用。

在 APF 的更新版本中将不再要求使用 ngcc。由于这些库的改变，开发人员可以期待更快的执行。

## 3.IE 11 支持已移除。

![](img/9320036164b0c3a0f4a9c16d264b63d7.png)

Photo by [Possessed Photography](https://unsplash.com/@possessedphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从版本 13 开始，Angular 将不再支持 Internet Explorer 11。放弃 Internet Explorer 11 会导致包更小，应用程序加载更快。此外，由于这些增强，Angular 现在可以通过本地 web APIs 使用现代浏览器功能，如 CSS 变量和 web 动画。

由于改进的 API 和缺乏 IE 专用的 polyfills，应用程序将加载更快。它还消除了对差动负载的需要。开发人员将受益于改进的 API 和基础设施，而应用程序用户将受益于更快的加载和更好的用户体验。

在项目迁移期间运行`ng update`将自动移除这些 IE 特定的聚合填充，从而减小包的大小。

## 4.TypeScript 4.4 兼容性

![](img/c1fb5605f26d7eb1b98ef856a0c95466.png)

Photo by [Andre Benz](https://unsplash.com/@trapnation?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Angular 13 版本中增加了对 TypeScript 4.4 的支持。因此，核心不再支持 4.4.2 之前的 TypeScript 版本。

**以下是 TypeScript 4.4 的主要特性:**

*   类型保护检测得到了改进
*   默认捕获变量
*   更快速的增量构建
*   可以检查条件的控制流
*   符号和模板字符串模式的索引签名

## 5.不再支持 12.20 之前的 Node.js 版本

![](img/6740014c5ff46f67d16c6fa3ce37a349.png)

Photo by [Aniket Bhattacharya](https://unsplash.com/@aniket940518?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Angular 13 不再支持 12.20.0 之前的 Node.js 版本。这是因为 Angular 包现在利用了 Node.js 包导出特性和子路径模式。

## 6.RxJS 版本 7.4

![](img/695205a62a62e62523a506454fa00991.png)

Photo by [Syed Rifat Hossain](https://unsplash.com/@syedrifathossain2002?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

RxJS 是 JavaScript 的一个反应式扩展，包含在 Angular 13 升级中，RxJS 的所有版本(包括版本 7)都包含在内。

RxJS 7.4 现在是用`ng new`创建的应用的默认版本。

现有 RxJS v6.x 应用程序必须使用 npm install rxjs@7.4 命令手动更新。你总是可以依靠 RxJS 7 来创建新的项目。现有项目应继续使用 RxJS 6。

## 7.路由器的变化

![](img/7c6857578bb762922208816dd018c826.png)

Photo by [José Martín Ramírez Carrasco](https://unsplash.com/@martinirc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

路由帮助我们从一个视图移动到另一个视图。它通过将浏览器 URL 解释为更改视图的请求来简化导航。

当新导航取消当前导航时，路由器不再使用最新更新更改浏览器 URL。

以前版本的 Angular 存在几个兼容性问题，主要是查询参数。例如，默认的 URL 序列化程序倾向于删除查询参数中问号后面的所有内容。相比之下，最近的更新提高了查询参数与问号的兼容性。

以前，`routerLink`指令的`null`和`undefined`输入等同于一个空字符串，没有办法阻止链接被导航。如果路由器链接指令值为`null`或`undefined`，导航将被完全禁用。

## 8.Angular CLI 的增强功能

![](img/a6a592159e7fb1cfffcd343aaefa3e87.png)

Photo by [Riccardo Annandale](https://unsplash.com/@pavement_special?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Angular CLI 是 Angular 拼图中最重要的一块。通过大规模降低复杂性，Angular CLI 有助于标准化处理现代 web 开发生态系统复杂性的过程。

随着 Angular 13 的发布，该框架现在提供了一个持久的构建缓存功能，该功能将内置结果保存到磁盘中作为默认功能。因此，发展进程将会加快。此外，您可以完全控制在当前角度项目中是否启用或禁用此功能。

## 9.角度测试得到了改进

![](img/30cb86b7b8f77825f8d858a4be3d0b65.png)

Photo by [Agence Olloweb](https://unsplash.com/@olloweb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

TestBed 已经被 Angular 团队更新了，现在可以在每次测试后正确地拆除测试环境和模块。

既然 DOM 在测试后被清除了，开发人员可能会期望更好的简化、更少的相互依赖、内存密集型和更快的测试。

## 10.创建动态组件

一种更简单的动态生成组件的技术是 Angular 13 中支持 Ivy 的 API 更新。为了构造一个组件，`ViewContainerRef.createComponent`不再需要实例化的工厂(你不再需要使用`ComponentFactoryResolver`)。

多亏了更新的`ViewContainerRef.createComponent` API，它现在能够用更少的样板代码生成动态组件。使用 Angular 以前的版本，这里有一个构建动态组件的例子。

```
@Directive({ … })
export class Test {
    constructor(private viewContainerRef: ViewContainerRef,
                private componentFactoryResolver: 
                        ComponentFactoryResolver) {}
    createMyComponent() {
        const componentFactory = this.componentFactoryResolver.
                             resolveComponentFactory(MyComponent);

        this.viewContainerRef.createComponent(componentFactory);
    }
}
```

使用 Angular 13 中的新 API，此代码将转换为以下内容:

```
@Directive({ … })
export class Test {
    constructor(private viewContainerRef: ViewContainerRef) {}
    createMyComponent() {
        this.viewContainerRef.createComponent(MyComponent);
    }
}
```

## 结论

你现在掌握了最新的角度 13 变化。如果你还在使用 Angular 12，是时候升级了，这样你就可以在下一个项目中利用新的功能。如果你已经安装了新版本，请在下面的评论区分享你的想法。

这就是这篇文章的内容。我希望你今天学到了一些新东西。想看更多这样的文章，敬请期待！

感谢阅读！

*更多内容尽在* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*