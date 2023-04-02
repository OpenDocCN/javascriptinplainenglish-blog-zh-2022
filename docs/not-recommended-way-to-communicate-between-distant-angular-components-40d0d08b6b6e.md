# 不推荐在远距离角度组件之间进行通信的方式

> 原文：<https://javascript.plainenglish.io/not-recommended-way-to-communicate-between-distant-angular-components-40d0d08b6b6e?source=collection_archive---------20----------------------->

## 在 Angular 应用程序中，当您需要时，实现一个快速而懒惰的解决方案来传递数据。

![](img/07a6c11d965dda69bdf5a695339a70d7.png)

Photo by [James Lee](https://unsplash.com/@picsbyjameslee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

官方 Angular 文档列出了[组件间通信的几种方式](https://angular.io/guide/component-interaction)。但是生活并不总是理想的。在一个晴朗的早晨，您仍然需要另一种交互方式，尤其是当组件松散地连接在一起，而您又懒得仅仅为了在它们之间交流而编写专用服务时。

在这些情况下，您可以使用 EventBus 模式。当心，不推荐，所以“*蜡烛带毛*”:)

# EventBusService

创建一个名为`EventBusService`的角度服务。该服务非常简单，有一个 RxJS 主题作为中介。

Event Bus Service

# 使用

从一个组件通过 EventBusService 引发事件:

```
export class FooterComponent {
  constructor(private ebs: EventBusService){} onClickAcceptCookie(): void {
    const event: CustomEvent = {
      key: 'USER_COOKIE_CONSENT',
      payload: {
        userId: "123", 
        acceptedOn: "2022-01-25T13:30:30Z"
      }
    } this.ebs.emit(event)
  }
}
```

在另一个组件中，拦截事件并采取行动:

```
public AdsComponent implements OnInit {
  constructor(private ebs: EventBusService){}ngOnInit(): void {
  this.ebs
      .on$('USER_COOKIE_CONSENT')
      .subscribe((payload) => bombardWithAds(payload));
  }
}
```

# 结论

事件监听从您订阅的那一刻起就开始了。所以要时刻关注小溪流了多久。当不再需要监听事件时，使用`take`、`takeUntil`操作符到流或`ngOnDestroy`钩子来终止订阅可能是个好主意。编码快乐！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***