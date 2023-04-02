# 控制反转:Typescript 中的服务定位器

> 原文：<https://javascript.plainenglish.io/inversion-of-control-service-locator-in-typescript-50d2d18a94a6?source=collection_archive---------8----------------------->

![](img/d8b6af07482922bf95562d28a106b0c5.png)

我已经在 Angular 工作了一段时间(超过 2 年)，自从我换到另一个工作场所，我就(大部分)转向了 Stencil。

Stencil 是一个非常好的生成 web 组件的 Typescript 编译器。如果我来放置它，它将是 Angular 和 React 之间的混合物。它像 Angular 一样使用[装饰器](https://stenciljs.com/docs/api)(让编译器收集元数据并基于此生成输出代码)，像 React 一样使用 [jsx/tsx](https://stenciljs.com/docs/templating-jsx) 和[生命周期](https://stenciljs.com/docs/component-lifecycle)。这是一个非常强大的工具来生成[设计系统](https://stenciljs.com/docs/design-systems)。

在我一直从事的这个设计系统中，有一个如何存储全局状态的问题。我想有一个类似于反转控制的版本(因为我真的很喜欢它在 [Angular](https://angular.io/guide/dependency-injection) )。使用 IoC 系统的最大好处是，您可以在测试中轻松地模拟服务，而不需要开玩笑地覆盖实际的导入(覆盖是好的，但是在复杂的设置中，您希望在迭代之间有不同的配置，这将变得混乱，因为如果在模拟之前有对模块的任何引用，模拟将不会工作)。

所以我想出了一个简单的全球可注射服务的解决方案，它不关心实际的实现。

第一步是考虑你想写的服务能做什么。基于此，您可以用服务的所有公共方法声明一个接口。让我们考虑一个设置和获取用户信息的简单服务。

The interface model for the user service

然后我们需要声明一个`UserServiceInstanceResolver`静态类，它将接收这个接口的类实现的实例，并存储它以便能够访问它。

Instance resolver for UserService

最后但同样重要的是，我们可以实现实际的服务

Actual implementation of UserService

最后，当你想实例化单件服务时，你可以这样做:

实际的好处是，每当你想测试任何使用这个实例的其他组件时，你可以很容易地在`UserServiceInstanceResolver.Instantiate`方法上实例化一个应用的模拟。

这就是我真正需要的(只是一个根级别的全局实例)。但是这段代码也可以扩展为支持每个组件实例(或层次结构实例),并获得更接近 Angular 的 DI 的体验。

感谢您阅读我的文章。如果你喜欢，请点击下面的按钮，让其他人也能看到。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **