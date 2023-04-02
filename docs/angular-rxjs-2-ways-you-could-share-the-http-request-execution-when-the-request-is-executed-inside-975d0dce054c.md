# Angular，RXJS:当请求在方法调用中执行时，共享 HTTP 请求执行的两种方式

> 原文：<https://javascript.plainenglish.io/angular-rxjs-2-ways-you-could-share-the-http-request-execution-when-the-request-is-executed-inside-975d0dce054c?source=collection_archive---------5----------------------->

![](img/8791140f420db29596a70759f2c34ac8.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我曾经写过一个类似的概念，您可以使用哪个多播操作符来确保 HTTP 请求只执行一次，并且在多个观察者之间共享响应，而不管他们何时订阅。

这里，HTTP 请求不在方法内部执行。

[](/typescript-rxjs-which-multicast-operator-can-be-used-for-sharing-http-request-between-multiple-ac0a349bd9c3) [## TypeScript，RXJS:使用哪个多播运算符来共享 HTTP 请求 b/w 多个观察器…

### RXJS 提供了许多操作符，哪一个操作符将满足您的要求，这肯定需要一些研究和…

javascript.plainenglish.io](/typescript-rxjs-which-multicast-operator-can-be-used-for-sharing-http-request-between-multiple-ac0a349bd9c3) 

这个故事略有不同。在 Angular 应用程序中，HTTP 请求执行发生在服务的方法内部。

多次调用该方法意味着有多个观察者订阅了该方法返回的可观察值。

**对于这些观察者中的每一个，都将执行一个单独的 HTTP 请求。**

如果 HTTP 请求在一个方法中执行，我如何防止它被多次执行？

**第一种方法:**

为了演示这个方法，我使用了一个组件 **HelloComponent** 和一个服务 **Method1Service。**

**方法 1 服务:**

**getUsers()** 是我们在其中执行 HTTP GET 请求以获取用户 Id 为 2 的用户的数据的方法。

我们没有将 **this.http.get()** 创建的可观察对象返回给调用 **getUsers()** 的组件，而是将这个可观察对象分配给我们定义的可观察对象 **userData$** 。

任何将 Method1Service 添加为依赖项的组件都可以访问 userData$ 。正确的做法应该是**将 userData$声明为** **private** 并通过 **public 方法访问它。我只是不想在例子中添加很多方法。尽量保持简单:)。**

我们使用了 **publishLast()+refCount()多播操作符**来确保来自 HTTP 请求的响应在观察者之间共享。

**HelloComponent 类:**

在 **ngOnInit()** 中，我们首先调用了 **getUsers()** ，用使用 **this.http.get()** 创建的可观察对象来重新分配 **userData$** 可观察对象。

接下来，我们调用了一个方法**creating observers for firstuserdata()**，其中我们创建了 2 个观察者，他们将订阅 **userData$** observable 来获取数据。第二个观察者在**延迟 1 秒**后订阅。

**getUsers()** 将只被**调用一次**到**执行一次 HTTP GET 请求**并将返回的可观察值赋给 **userData$。**此后，任何想要该数据的组件只需订阅 **userData$。**

**第二种方法:**

为了演示这个方法，我使用了一个组件 **HiComponent** 和一个服务 **Method2Service** 。

**Method2Service:** 现在，你只需要知道这个服务的 2 点:= >服务定义了一个**behavior subject userdata subject $**，初始值为 **null** 。

= >该服务定义了一个 **getUsers()** ，它执行一个 HTTP GET 请求来获取一个用户 Id 为**3**的用户的数据。

这两点是如何协同工作的，我们将在查看 **HiComponent 类**后进行检查。

**HiComponent 类:**

在 **ngOnInit()** 中，我们首先调用了 **Method2Service** 的 **getUsers()** ，它可以返回两个值中的任意一个:

= >由 **this.http.get()** 在 **Method2Service** 中创建的可观察对象。

运筹学

= >操作员的 rxjs **创建的冷可观察值。**该操作符将发出由 **Method2Service 中的主题 **userDataSubject$** 持有的值。**

接下来，我们调用了方法**creating observersforseconduserdata()**，其中我们创建了 2 个观察器，它们将订阅由 **getUsers()** 返回的可观察对象以获取数据。第二个观察者在**延迟 3 秒**后订阅。

**策略:**

= >在**方法 2 服务**中的**用户数据主体$** 是一个**行为主体**，其**初始值为空**。当有观察者订阅该主题，但该主题尚未发出值时，会向观察者发出该值。

= >当 **HiComponent** 类第一次调用 **getUsers()** 时，即当第一个观察者订阅了 **getUsers()** 返回的可观察对象时， **userDataSubject$** subject 的 value 属性将为空。

因此，控制转到 **getUsers()** 中的 ELSE 块，并执行 HTTP GET 请求。

```
else {
**return this.http.get(‘https://jsonplaceholder.typicode.com/users/3')**.pipe(
tap((y) => console.log(‘Emitting value’)),
map((x) => x),
catchError((err) => throwError(err))
);
}
```

当请求成功完成时，第一个观察者的 **next()回调**被执行，在这个回调中，我们记录了响应，并对 **userDataSubject$调用了 **next()** 。**

```
**this.method2Service.userDataSubject$.next(value);**
```

= >当 **HiComponent** 类下次调用 **getUsers()** 时，**userdata subject $**subject 的 value 属性将包含用户数据，因此控件将在 IF 块本身中。

```
if (this.userDataSubject$.value) {
**return of(this.userDataSubject$.value);**
}
```

操作员的 **rxjs 创建的冷可观察值将返回到组件。这个可观察对象将向第二个观察者发出 userDataSubject$** 的**值。**

这样，我们避免了额外的 HTTP 请求，并与多个观察者共享单个 HTTP 请求执行的响应。

您可以在下面找到完整的工作示例。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*