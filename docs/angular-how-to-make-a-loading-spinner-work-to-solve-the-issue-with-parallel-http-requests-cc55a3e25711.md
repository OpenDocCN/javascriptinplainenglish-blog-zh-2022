# Angular:如何使用加载微调器来解决并行 Http 请求的问题

> 原文：<https://javascript.plainenglish.io/angular-how-to-make-a-loading-spinner-work-to-solve-the-issue-with-parallel-http-requests-cc55a3e25711?source=collection_archive---------2----------------------->

可以在根组件和/或子组件级别添加加载微调器，以向用户指示任何请求的进度。

![](img/d49343a306455e69b196e18215a62044.png)

无论您将它添加到哪里:

= >整个应用程序的根组件级别有一个通用微调器

运筹学

= >每个组件 1 个微调器

有一个常见问题。让我列出问题的步骤。

1.  我有许多并行运行的 http 请求。
2.  在每个请求开始之前，微调器启动，在每个请求结束之后，微调器隐藏。
3.  有可能请求 A 即将完成，而请求 B 开始。只要两者都在进行中，微调器就会一直运行。但是当请求 A 完成时，它将隐藏微调器，即使请求 B 仍在进行中。

我们如何告诉 Angular，**只要至少有一个 http 请求正在进行，就不要隐藏微调器**？

= >一种可能性是在**拦截器级别**处理。拦截器级别的处理也意味着整个应用程序只能有一个通用的 spinner。

模态/对话只不过是另一个组件，是打开它的组件的子组件。

你可能会问我如何将这种方法扩展到情态动词/对话？在这个场景中，**一旦模态被执行/提交，**就让**将 http 请求执行从模态传递给它的父组件来处理它**。

= >如果您不希望在拦截器级别处理它，下一个选项是使用 **RXJS mergeMap、merge、forkJoin** 操作符对要并行执行的 API 调用进行分组。这确保了当 API 调用开始执行时微调器开始显示，并且只有在所有调用都完成执行(成功/错误)后，加载微调器才会隐藏。

下面是一个使用 forkJoin 和 merge 操作符并行执行 4 个 API 调用的例子。在第一个和第二个 API 调用开始执行之前，我引入了 5 秒和 2 秒的延迟。第三和第四个 API 调用立即开始执行。**延迟的目的是为了表明，直到所有的 API 调用没有成功/错误地完成，微调器不会隐藏。**

使用**叉连接**:

![](img/88b58a5ef3ea9504efe74f8b8e47ced3.png)

使用**合并**:

![](img/fd2baa7c060d6cdbc5a8c910e7d5724f.png)[](https://stackblitz.com/edit/angular-sbuqbb?file=src/app/app.component.ts) [## 角形(叉形)堆叠

### 基于@angular/animations、@angular/common、@angular/compiler、@angular/core、@angular/forms 的 angular-cli 项目…

stackblitz.com](https://stackblitz.com/edit/angular-sbuqbb?file=src/app/app.component.ts) 

以上是这种方法的工作示例。

我没有详细介绍这一点，因为在这个故事中，我想更多地关注在拦截器级别处理它的第一种方法。

现在让我们继续讨论拦截机的方法。

这是一个简单的项目，我将演示如何使用一个加载微调器来指示多个 Http 请求的进行中状态。

让我们从**拦截器**和 **SpinnerService** 开始，来理解我们如何解决并行 http 请求的问题。

**纺纱服务。**该服务的目的主要是处理装载旋转器的隐藏/显示。它还处理 Http 请求失败时遇到的错误消息的显示。

```
@Injectable({ providedIn: ‘root’ })
export class SpinnerService {
constructor() {}

private spinnerSub$ = new BehaviorSubject<boolean>(false);
private errSub$ = new Subject<any>();
errObsv$ = this.errSub$.asObservable()
.pipe(scan((acc, curr) => (acc = acc.concat(curr)), []));

spinnerObsv$ = this.spinnerSub$.asObservable();

toggleLoadingSpinner(status: boolean) {
this.spinnerSub$.next(status);
}

pushMessage(err: any) {
this.errSub$.next(err);
}
}
```

这个想法很简单。

= >分别有一个**私有主题**用于处理加载微调器和错误，即 **spinnerSub$和 errrSub$** 。

= >我们已经提供了**公共方法**来允许组件/拦截器将数据传递给**主题**，即 **toggleLoadingSpinner()** 和 **pushMessage()。**

= >我们还创建了一个对应于每个**私有主题**的**公共可观察对象**，即 **spinnerObsv$** 和 **errObsv$。**这使得****组件能够访问这个可观察的**并决定是否显示/隐藏微调器和显示错误信息。**

**向**拦截器**移动。这可能看起来很大，但概念很简单:**

**"只要至少有一个请求正在进行，就显示微调器。当所有请求完成执行(成功/失败)时隐藏微调器"**

```
interface UniqueRequest {
uniqueRequestIdentifier: number;
req: HttpRequest<any>;
}

@Injectable()
export class SpinningInterceptorService implements HttpInterceptor {
constructor(private service: SpinnerService) {}

inProgressRequests: UniqueRequest[] = [];
uniqueRequestIdentifier: number = 0;

removeRequest(modifiedReq: UniqueRequest) {
let areRequestsPending: boolean = false;

let reqIndex = this.inProgressRequests.findIndex((x) =>
x.req.url === modifiedReq.req.url &&
x.req.method === modifiedReq.req.method &&
x.uniqueRequestIdentifier === modifiedReq.uniqueRequestIdentifier
);

if (reqIndex > -1) {
this.inProgressRequests.splice(reqIndex, 1);
}
areRequestsPending = this.inProgressRequests.length > 0;
this.service.toggleLoadingSpinner(areRequestsPending);
}

addRequest(modifiedReq: UniqueRequest) {
this.inProgressRequests.push(modifiedReq);
this.service.toggleLoadingSpinner(true);
}

intercept(req: HttpRequest<any>,next: HttpHandler): Observable<HttpEvent<any>> {
this.uniqueRequestIdentifier = this.uniqueRequestIdentifier + 1;
let modifiedReq = {
…{ uniqueRequestIdentifier: this.uniqueRequestIdentifier },
…{ req: req },
};
this.addRequest(modifiedReq);

return next.handle(req).pipe(
delay(2000),
finalize(() => {
//error or success : remove the request
this.removeRequest(modifiedReq);
})
);
}
}
```

1.  ****inProgressRequests** 属性是一个类型为 **UniqueRequest** 的对象数组。**

```
 inProgressRequests: UniqueRequest[] = [];
  uniqueRequestIdentifier: number = 0;
```

**查看接口，我们知道每个对象将包含一个 **req 属性**，它是实际的 **HttpRequest** 和一个**uniqueRequestIdentifier**属性，它只是分配给每个请求的一个数字。编号的目的只是为了在多个 HttpRequest 的 url 和方法相同的情况下给对象增加一些唯一性。**

```
interface UniqueRequest {
uniqueRequestIdentifier: number;
req: HttpRequest<any>;
}
```

**所以**对象属性 req** 只不过是 HttpRequest，对象属性**uniqueRequestIdentifier**从类属性 **uniqueRequestIdentifier 获取其值。****

**2.从**截距()**开始，**

```
intercept(req: HttpRequest<any>,next: HttpHandler): Observable<HttpEvent<any>> {
this.uniqueRequestIdentifier = this.uniqueRequestIdentifier + 1;
let modifiedReq = {
…{ uniqueRequestIdentifier: this.uniqueRequestIdentifier },
…{ req: req },
};
this.addRequest(modifiedReq);

return next.handle(req).pipe(
delay(2000),
finalize(() => {
//error or success : remove the request
this.removeRequest(modifiedReq);
})
);
}
```

**在这个方法中，我们首先增加类属性**uniqueRequestIdentifier**来为请求创建一个新的标识符。**

**接下来，我们将 http req 对象 **req** 和类属性**uniqueRequestIdentifier**添加到新对象 **modifiedReq** 中。**

**下一步是调用 **addRequest()** ，将对象 **modifiedReq** 作为参数传递。在这个方法中，我们将对象 **modifiedReq** 推入 **inProgressRequests** 数组，然后调用 **SpinnerService** 的 **toggleLoadingSpinner()** 来开始显示加载微调器。请注意，我们已经将 **true** 作为参数传递给了 **toggleLoadingSpinner()** ，以指示请求即将开始，微调器需要显示。**

```
addRequest(modifiedReq: UniqueRequest) {
this.inProgressRequests.push(modifiedReq);
this.service.toggleLoadingSpinner(true);
}
```

**回到 intercept()，注意我们已经将 **delay()** 和 **finalize()** rxjs 操作符通过管道传递给 HttpRequest 返回的可观察对象。**

```
return next.handle(req).pipe(
delay(2000),
finalize(() => {
//error or success : remove the request
this.removeRequest(modifiedReq);
})
);
```

**delay()操作符的目的只是添加一个 2 秒的延迟，以便可以清楚地看到微调器。**

**不管 HttpRequest 是成功还是失败，finalize() 操作符都会执行。在这两种情况下，我们都需要隐藏微调器。因此，此时调用 **removeRequest()** ，将 **modifiedReq 对象**作为参数传递。**

```
removeRequest(modifiedReq: UniqueRequest) {
let areRequestsPending: boolean = false;

let reqIndex = this.inProgressRequests.findIndex((x) =>
x.req.url === modifiedReq.req.url &&
x.req.method === modifiedReq.req.method &&
x.uniqueRequestIdentifier === modifiedReq.uniqueRequestIdentifier
);

if (reqIndex > -1) {
this.inProgressRequests.splice(reqIndex, 1);
}
areRequestsPending = this.inProgressRequests.length > 0;
this.service.toggleLoadingSpinner(areRequestsPending);
}
```

**在 **removeRequest()** 中，我们首先根据请求的 url、方法和 uniqueRequestIdenfier 值在 **inProgressRequests** 数组中定位请求。接下来，我们从数组中删除找到的请求。**

**此时，如果 **inProgressRequests** 数组为空，则意味着当前**没有其他请求正在进行**，我们可以调用 SpinnerService 的 **toggleLoadingSpinner()** ，传递 **false** 作为参数来隐藏微调器。**

**如果 i **nProgressRequests** 数组不为空，这意味着还有其他请求正在进行中，我们必须通过将 **true** 作为参数传递给 SpinnerService 的 **toggleLoadingSpinner()** 来继续显示 spinner。**

**下面是工作示例。**

**[](https://stackblitz.com/edit/angular-oc1fxl?file=src/app/spinning-interceptor.service.ts) [## 角形(叉形)堆叠

### 基于@angular/animations、@angular/common、@angular/compiler、@angular/core、@angular/forms 的 angular-cli 项目…

stackblitz.com](https://stackblitz.com/edit/angular-oc1fxl?file=src/app/spinning-interceptor.service.ts) 

在这个例子中，我们在 **AppComponent** 中并行获取了假的**相册**和**照片**数据。您可以尝试更改 Http 请求的开始和结束时间，以检查 spinner 在不同场景中的工作方式。

如果你有兴趣知道我们如何使用同一个 spinner 来一起跟踪 Http 请求进度和组件导航，请查看下面的故事。

[](https://ramya-bala221190.medium.com/showing-a-simple-spinner-when-loading-components-server-data-in-angular-fcc3a1c505ee) [## 显示了在 Angular 中加载组件/服务器数据时的简单微调器

### 旋转器/加载器使用户体验更加流畅，因为他知道视图正在加载，并且有…

ramya-bala221190.medium.com](https://ramya-bala221190.medium.com/showing-a-simple-spinner-when-loading-components-server-data-in-angular-fcc3a1c505ee) 

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[*YouTube****，以及***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。***