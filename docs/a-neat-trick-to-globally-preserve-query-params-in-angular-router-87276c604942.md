# 角度路由器中全局保存查询参数的巧妙方法

> 原文：<https://javascript.plainenglish.io/a-neat-trick-to-globally-preserve-query-params-in-angular-router-87276c604942?source=collection_archive---------4----------------------->

![](img/52bbf4082f7a5c5a2df104642754b82b.png)

Photo Credits: Author

角路由器是软件工程的奇迹。它基于网络导航的简单原则。

*   URL 只不过是一个序列化的树。这意味着您可以将 URL 反序列化为表示它的树。
*   URL 是 web 应用程序的唯一来源(嗯…应该是！)
*   路由是一种可能的路由器配置
*   每个路由器配置都是一棵树，可以序列化为一个 URL

![](img/c28da773d5a30b6f560b15823194f775.png)

目前，没有办法在所有路线导航中全局保留查询参数。例如，如果您正在检查 URL 中是否存在一个`token`，以验证用户是否可以深度链接到一个 URL。我们可以通过使用古老的策略模式和依赖注入来实现这一点。

# 扩展路由器的默认位置策略

```
import { PathLocationStrategy, APP_BASE_HREF, PlatformLocation } from '@angular/common';
import { Optional, Inject, Injectable } from '@angular/core';
import { UrlSerializer } from '@angular/router';@Injectable()
export class PathPreserveQueryLocationStrategy extends PathLocationStrategy {
  private get search(): string {
    return this.platformLocation?.search ?? '';
  }
  constructor(
    private platformLocation: PlatformLocation,
    private urlSerializer: UrlSerializer,
    @Optional() @Inject(APP_BASE_HREF) _baseHref?: string,
  ) {
    super(platformLocation, _baseHref);
  } prepareExternalUrl(internal: string): string {
    const path = super.prepareExternalUrl(internal);
    const existingURLSearchParams = new URLSearchParams(this.search); const existingQueryParams = Object.fromEntries(existingURLSearchParams.entries());
    const urlTree = this.urlSerializer.parse(path);
    const nextQueryParams = urlTree.queryParams; urlTree.queryParams = { ...existingQueryParams, ...nextQueryParams }; return urlTree.toString();
  }
}
```

# 解释:

*   我们扩展默认的`PathLocationStrategy`类来实现我们的查询参数保存算法
*   我们覆盖了`prepareExternalUrl`方法来处理 URL 中的查询参数
*   我们获取现有的 URLSearch 参数作为`[URLSearchParams](<https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams>)`的实例
*   我们从路径中创建一个`[URLTree](<https://angular.io/api/router/UrlTree>)`，合并现有的和新的查询参数，并将其分配给新创建的 URL 树的`queryParams`
*   我们序列化新创建的 URL 树，并将其作为字符串返回

# 提供定制定位策略

```
// app.module.tsimport { LocationStrategy } from "@angular/common";
import { PathPreserveQueryLocationStrategy } from "./preserve-query-params.ts";@NgModule({
...
providers: [
    { provide: LocationStrategy, useClass: PathPreserveQueryLocationStrategy }
  ],
...
})
export class AppModule {}
```

# 更新 Dom.iterable 实用程序的 TS 配置

将以下配置添加到项目根目录下的`tsconfig.json`文件中。我们需要这个来使`URLSearchParams`类和`.entries()`方法在我们的项目中可用

```
// tsconfig.json
{
  "compilerOptions": {
		...
    "downlevelIteration": true,
    "lib": [
      "es2019",
      "dom",
      "dom.iterable",
      "ESNext"
    ]
	...
  }
}
```

# 警告

*   由于所有查询参数都会保留，因此一旦将查询参数添加到路径中，所有后续导航都会携带该参数

# 结论

我们学习了如何在角度路由器中全局保存查询参数。我们看到 Angular 的依赖注入系统是多么强大，我们利用它来覆盖 Angular 的默认定位策略。

下面是一个代码沙箱，其中有一个工作示例:

[角度保留查询参数](https://codesandbox.io/s/angular-preserve-query-params-up6cs?file=/src/app/app.component.ts)

感谢你的阅读，我希望这能帮助你，就像它帮助了我一样。

我很想在下面的评论中知道这是否有用！

你可以在 [GitHub](https://github.com/nivrith) 或者 [Twitter](https://twitter.com/_Nivrith_) 上关注我

快乐工程！

***如果你想更新更多类似的文章*** [***订阅我的简讯***](https://resources.bytelimes.com/)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*