# 如何在 Angular 应用程序启动前加载数据

> 原文：<https://javascript.plainenglish.io/how-to-load-data-before-your-angular-app-starts-71083cf56132?source=collection_archive---------2----------------------->

## 使用 APP_INITIALIZER

![](img/347df6f1fa807c9cc3d50d7d445dff77.png)

Photo by [Dayne Topkin](https://unsplash.com/@dtopkin1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在应用程序启动之前，是否必须加载配置文件来设置一些应用程序属性或加载一些数据？我们来看看有角的怎么做。在我们开始之前，先快速回顾一下 Angular 应用程序如何通过 6 个步骤启动:

# 自举过程

1.  加载 index.html
2.  加载 Angular、其他库和应用程序代码
3.  执行 main.ts 文件
4.  加载应用模块
5.  加载应用程序组件
6.  流程模板

HTML 文件有`<app-root></app-root>`标签，Angular 在这里注入我们的应用程序。

Angular 基于模块和 DI(依赖注入)系统。所以在`main.ts`中，我们有`bootstrapModule()`，它将主应用程序模块作为一个参数，并为给定的平台创建它的一个实例:

`main.ts`

```
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';import { AppModule } from './app/app.module';
import { environment } from './environments/environment';if (environment.production) {
  enableProdMode();
}platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

App module(与任何其他 Angular module 一样)包含声明、导入、提供程序，还包含入口组件，这是一个默认的 AppComponent。

```
bootstrap: [AppComponent]
```

然后，组件被加载并呈现在页面上。现在我们已经了解了这个过程，让我们回到主题。app 启动前如何加载数据？考虑到开头列出的步骤，我们可以说我们必须在步骤 4 和 5 之间进行干预。

*   (4)加载应用模块
*   →在 providers 数组中使用 APP_INITIALIZER 标记
*   (5)加载应用程序组件

# APP_INITIALIZER 令牌

它是阿迪令牌，可以用来提供一个或多个初始化函数。在`app.module.ts`中，我们必须通过以下方式提供它:

```
import { NgModule, APP_INITIALIZER } from '@angular/core';
// other imports...@NgModule({
 imports: [BrowserModule],
 declarations: [AppComponent],
 bootstrap: [AppComponent],
 providers: [{
   **provide: APP_INITIALIZER,
   useFactory: () => appConfigFactory
   deps: [AppInitService],
   multi: true**
  }]
 })
export class AppModule {}
```

在 providers 数组中，我们传入 APP_INITIALIZER 令牌，并在`useFactory`属性中定义一个名为`appConfigFactory`(当然名称由您决定)的函数。数组可以是空的，但是你可以在这里传递任何你需要的服务。更准确地说，是工厂功能所依赖的服务。`multi: true`意味着我们可以定义更多的应用初始化器。

Angular 的[源代码中是这样定义令牌的:](https://github.com/angular/angular/blob/13.2.0/packages/core/src/application_init.ts#L86-L87)

```
export const APP_INITIALIZER =
    new InjectionToken<ReadonlyArray<() => Observable<unknown>| Promise<unknown>| void>>('Application Initializer');
```

这告诉我们，我们必须回报一个承诺或一个可观察的。

## 工厂(初始化)功能

> 提供的函数在应用程序启动时注入，并在应用程序初始化期间执行。如果这些函数中的任何一个返回一个承诺或一个可观察值，那么直到承诺被解析或可观察值被完成，初始化才完成。

上述工厂函数的一个基本示例如下所示。(注意，该功能也可以直接在`app.module.ts`文件中定义，而不是在单独的文件中定义)

```
import { AppInitService } from './../services/app-init.service';export function appConfigFactory(appInitService: AppInitService) {
  return (): Promise<any> => {
    return appInitService.init()
  }
}
```

还请注意，我们在`deps`数组中定义的`AppInitService`被用在工厂函数中，在这里我们从它调用一个‘init()’方法。在那里你可以实现任何你需要的逻辑。例如，您可以使用 httpClient 加载一个包含一些数据的 JSON 文件来配置您的应用程序。

# 结论

我们学习了如何在模块中利用 APP_INITIALIZER 令牌及其初始化函数，以便在应用程序组件被初始化和呈现之前执行一些步骤。这比直接在组件和组件模板中处理逻辑/加载文件更好。

**资源/实例:**

[棱角分明的文档](https://angular.io/api/core/APP_INITIALIZER)

【Angular 应用的编译时与运行时配置

[在 Angular 中引导应用](https://www.pluralsight.com/guides/bootstrapping-an-application-in-angular)

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***