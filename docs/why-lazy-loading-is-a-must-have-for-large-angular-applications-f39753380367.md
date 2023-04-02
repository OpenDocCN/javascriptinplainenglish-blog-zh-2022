# 为什么延迟加载是大角度应用的必备条件

> 原文：<https://javascript.plainenglish.io/why-lazy-loading-is-a-must-have-for-large-angular-applications-f39753380367?source=collection_archive---------15----------------------->

![](img/dd6c74cedc9c7404d22b350c4352a378.png)

Lazy loading in Angular

通过只在需要时加载应用程序的特定组件，延迟加载的方法有助于 web 应用程序更好地执行。利用 Angular 的路由器功能，可以实现延迟加载。

在这篇文章中，我们将研究惰性加载是如何工作的，以及如何使用它来提高 Angular 应用程序的性能。它可以提供的不同优势将在接下来的章节中详细介绍。

# 什么是懒装？

> Lazy loading 是 Angular 中的一项技术，允许您在特定路由被激活时异步加载 JavaScript 组件。

大型的 Angular 应用程序从延迟加载中受益匪浅，因为它允许你将应用程序分成更容易管理的、更小的部分，可以根据需要加载。这可以大大加快应用程序的初始加载时间，并全面提升用户体验。

并非所有用户都可以使用具有众多功能的应用程序，这些功能可以从延迟加载中获益。例如，如果您的应用程序包含只有少数客户使用的仪表板功能，那么您可以利用延迟加载，只在用户导航到仪表板时加载，而不是一次为所有用户加载。

对于任何想要优化应用程序的开发人员来说，延迟加载都是必不可少的，因为它可以极大地提高大角度应用程序的性能和用户体验。

延迟加载在角度应用中有很多好处:

1.  **改进的性能**:通过将你的程序分成更小的、可按需加载的部分，你可以大大减少应用程序初始加载的时间，并提高整体性能。
2.  **改进的 SEO** :由于搜索引擎偏爱加载速度快的网站，你可以通过缩短应用程序初始加载的时间来提升你在搜索引擎中的排名。
3.  **增强的可扩展性**:通过添加额外的特性和功能而不显著延长应用的初始加载时间，延迟加载可以帮助您的应用更成功地扩展。
4.  **更好的用户体验**:通过减少应用程序的初始加载时间，用户将能够更快地使用它，这可以从整体上改善用户体验。
5.  更容易维护:通过将你的应用分成更小、更容易管理的模块，延迟加载使得随着时间的推移维护和更新你的代码变得更加容易。

以下是如何使用 Angular 路由器在 Angular 应用程序中实现延迟加载的示例:

您必须首先将您的路由配置为使用延迟加载。路由配置对象的`loadChildren`属性可用于此:

```
const routes: Routes = [
  {
    path: 'dashboard',
    loadChildren: () => import('./lazy/dashboard.module')
    .then(m => m.DashboardModule)
  }
];
```

产生承诺的函数应该是`loadChildren`属性的值，该承诺与应该延迟加载的模块一起解析。在这种情况下，LazyModule 是异步导入的，一旦路由激活，就会被加载。

下一步是导入`RouterModule`并使用`forRoot`方法配置路由:

```
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

最后，您可以使用`routerLink`指令链接到模板中的延迟加载路由:

```
<a [routerLink]="['/dashboard']">Dashboard</a>
```

当用户点击链接时,`DashboardModule`将被加载并且路线将被触发。

## 结论:

总之，惰性加载是一种可以显著提高大角度应用程序的性能和用户体验的技术。通过将应用程序分成更小、更易于管理、可以按需加载的块，您可以减少应用程序的初始加载时间，并提高整体性能。

我希望这篇文章对你有所帮助。 ***感谢阅读。***

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)*

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*