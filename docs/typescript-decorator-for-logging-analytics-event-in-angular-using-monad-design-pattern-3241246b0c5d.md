# 使用 Monad 设计模式在 Angular 中记录分析事件的 TypeScript 装饰器

> 原文：<https://javascript.plainenglish.io/typescript-decorator-for-logging-analytics-event-in-angular-using-monad-design-pattern-3241246b0c5d?source=collection_archive---------0----------------------->

## Logging Decorator 使用 Monad 设计模式、解耦应用程序代码和日志逻辑来跟踪 Angular 中的分析事件。

![](img/97aa9ff941f495a649078bc4b75c07c0.png)

Monads, Monads Everywhere

在每个 web/移动应用程序中，当它扩展时，会有一个点需要记录 API、用户行为跟踪、事件、分析、错误等。

日志记录是在问题影响您的用户或组织之前进行故障排除和解决问题的最佳实践。

要做到这一点，对于每一个事件动作，你需要将事件分派到分析平台，比如 Google analytics。

假设您有一个函数`logEvent`,它将分析事件发送到如下服务:

```
interface IEvent = {
  eventName: string;
  eventData: {
    args: any;
   };
}const logEvent = (event: IEvent) => {
  thirdPartyAnalyticsService.send(event)
}const getUser = (userId) => {
 logEvent({eventName: 'submit'; eventData: { args: userId }}); result = getUserFromAPI() // .... do some operations
 return result;
}
```

如果你看上面的代码，你会很快注意到代码库将充满方法`logEvent`混乱和重复无处不在，因为需求不断变化，很快就会有很多条件和混乱。

这开始真的真的伤害你的眼睛，你开始在你的梦里看到`logEvent`。😴哦，噩梦。😱

很长一段时间，当我偶然发现`Monads`时，我正在寻找一种解决方案来干燥这段代码，这就是点开始连接的时候。👀

这里有一个视频很好地解释了单子是什么:[https://www.youtube.com/watch?v=C2w45qRc3aU](https://www.youtube.com/watch?v=C2w45qRc3aU)

> 基本上，单子是一种设计模式，允许用户链接操作，同时单子在幕后管理秘密工作。

这正是我们想要的，在幕后秘密地进行记录。🤐

## 单子有三个部分:

1.  包装类型
2.  包裹功能:允许进入单子生态系统
3.  运行函数:对一元值运行转换

但这和我们的问题有关系吗？让我们看看如何使用包装函数来解决这个问题。

这是一个高阶函数，稍微做了一点调整，我们也跟踪原始函数的结果。

如果你仔细观察`logWrapper`功能，铃声开始响起，叮，丁丁，叮，叮…🔔

![](img/7a83437c0d35887294178b1d1555d6d1.png)

> 瞧，装饰者们…

这个函数看起来更像装饰者…🔮

![](img/6f80beab6988c6b26cc1421d5da03f7a.png)

所以你可能想知道装饰者和单子是不是一样的，简而言之它们不是。但这是以后的话题。🗣

回到我们的问题，模式看起来有点类似，我们可以创建一个`logEvent`自定义的 typescript 方法装饰器，它完全满足相同的目的。代码将类似于下面这样。

通过上述方法，我们隔离了应用程序和分析代码。

虽然上面的代码看起来很完整，解决方案也运行良好，但是它有一些限制。考虑以下场景:

```
@Logger()
getUser(userId) {
  // say some extra data is required to perform api request and we 
  // also need to track that extra data.
  const randomExtraData = Math.random(); const result = getUserFromAPI(userId, randomExtraData);
  return result;
}
```

在上面的例子中，我们的`Logger`装饰者可以访问`userId`和`result`，但是不能访问`randomExtraData`。

使用我们现有的实现，我们将无法捕获`randomExtraData`的值，并将其包含在传递给`logEvent`的分析事件中。

换句话说，在应用程序代码函数体中构造的数据对`logEvent`函数不可用，也不能包含在跟踪事件中。

这个随机数据可以是任何东西，另一个函数调用的结果、网络请求、修改的数据等等。

为了实现这一点，我们需要做一些改变。

因为`Logger`可以访问它所调用的函数的返回值，所以我们可以通过将返回类型从数字改为对象，在返回值中传递一些内部数据(在本例中为`randomExtraData`)。

*接下来是我们创建“WrapperType”的部分。*

```
[@Logger](http://twitter.com/Logger)()
getUser(userId) {
  const randomExtraData = Math.random(); const result = getUserFromAPI(userId, randomExtraData);
  return {
     result: result,
     __loggingInfo: {
        eventName: 'getUserEvent',
        eventData: {
          args: userId,
          result: result,
          extraData: randomExtraData,
        },
     } as IEvent
  }
}
```

很好，解决了一个问题，但是有时我想在记录之前向现有的事件数据中添加额外的数据，或者对 event data 进行一些更改，但有时我不想这样做。

这个数据修改过程是特定于日志记录的，我不希望我的组件了解它，甚至不希望处理它。

为了解决这个问题，我们可以在我们的`Logger`装饰器中引入一个参数，它可以接受一个*构造函数*，该函数构造一个定制的分析事件有效负载，可能会添加一些额外的数据。

让我们看看这个的最终结果。

***记录器装饰器实现:***

***应用组件利用记录器装饰器:***

此外，这里是展示上述记录器装饰器的 **Stackblitz 示例**，请继续查看。💻

[](https://stackblitz.com/edit/angular-ivy-2gym2w?file=src/app/app.component.ts) [## 萨达斯

### 基于@angular/animations、@angular/compiler、@angular/core、@angular/common 的 angular-cli 项目…

stackblitz.com](https://stackblitz.com/edit/angular-ivy-2gym2w?file=src/app/app.component.ts) 

最后，我们简要讨论了 Logger decorator 的实现，该实现用于使用 TypeScript decorator 在 Angular 中跟踪分析数据。

请在下面留下评论，让我知道其他各种方法，如果有的话，或者如果有任何即兴创作。我很乐意回答这些问题。

**参考文献:**

1.  [建造单子](https://sambernheim.com/blog/building-a-monad)🗒[塞缪尔·伯恩海姆](https://mobile.twitter.com/sambernheim)
2.  [【Youtube】软件工程师对单子的最佳介绍](https://youtu.be/C2w45qRc3aU)📹

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。****