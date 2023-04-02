# 如何在 Angular 中创建可扩展的 API 服务

> 原文：<https://javascript.plainenglish.io/how-to-create-an-extensible-api-service-in-angular-e451073a2f90?source=collection_archive---------5----------------------->

![](img/c346cf26c861e327f650c3324a3d3e73.png)

如果你正在创建一个有角度的前端网站，你无疑会利用 API。让我们来看看一种简单的方法，可以标准化您的 API 服务，以及处理它们可能收到的任何响应错误。

我的前端站点通常会使用不止一个 API。因此，我更喜欢为每个 API 端点创建一个服务，并在需要的地方注入它们。为了防止重复代码，我总是创建一个基础`api.service.ts`,我的其他 API 服务将扩展这个基础。基类看起来像这样:

本质上，该类包含了可能需要从 API 请求的每个 RESTful 操作的方法。对于这个例子，我只展示了 GET 和 POST，但是 PUT、DELETE 和 PATCH 也可以按照相同的范例添加。

我们当然使用 Angular 的 HttpClient 来发送请求。此外，我们正在利用 RxJS 内置的`pipe()`和`tap()`函数。通过使用`tap()`,我们可以拦截响应并处理任何可能返回的错误，并且仍然将响应发送给最初调用它的服务。通过在父 API 类中这样做，并让每个子服务调用这些函数，我们确保每个错误都被捕获和处理。然而，还有另一种方法可以达到同样的效果。通过实现 Angular 的 HttpInterceptor 类，可以用类似的方式处理传出的请求和响应。我更喜欢可扩展服务方法。

现在我们有了基类，我们可以为我们可能需要向其发送请求的每个 API 创建一个服务类。这里有一个例子:

这个基本的示例服务有一个发出 GET 请求的函数和一个发出 POST 请求的函数。因为所有的工作都是在父类中完成的，所以这个子服务只需要从父类中调用相应的函数并返回它的承诺。

使用这种方法，我们创建的任何 API 服务都可以非常简单和干净地扩展父 API 并到达一个 API，而不用担心每个 API 的错误捕获。

我希望这个方法对你有所帮助，并一如既往地感谢你的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*