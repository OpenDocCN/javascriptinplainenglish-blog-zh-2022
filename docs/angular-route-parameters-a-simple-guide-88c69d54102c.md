# 角度布线参数:简单指南

> 原文：<https://javascript.plainenglish.io/angular-route-parameters-a-simple-guide-88c69d54102c?source=collection_archive---------1----------------------->

## Angular 的布线参数以及如何在布线元件之间传递小块信息的概述。

![](img/60d6465af57bd11b28e9d9dba3f62b13.png)

Photo by author

路由是 Angular 中的基本机制之一。它的主要用途是提供一种在应用程序中导航的方法。没有它，我们将永远停留在同一页上！

除了导航之外，路由还可以用于在路由组件之间传递小块信息。这可以通过使用 ***路线参数*** 来实现。

Angular 中有三种类型的布线参数:

*   必需的参数，
*   可选参数，和
*   查询参数。

在本文中，我们将介绍基本路由的工作原理。然后我们研究 Angular 提供的所有三种类型的路线参数。

我们开始吧！

# 路由基础

路由主要用于在应用程序中导航。大多数单页应用程序都有某种菜单(或工具栏),这样用户就可以四处导航。

为了实现导航，我们在菜单的 HTML 中使用了`[RouterLink](https://angular.io/api/router/RouterLink)`指令。`routerLink`定义了当用户点击特定选项时将被激活的路线。

```
<div>
  <ul>
    <li><a [routerLink]="['/home']">Home</a></li>
    <li><a [routerLink]="['/pandas']">Pandas</a></li>
  </ul>
  <router-outlet></router-outlet>
</div>
```

假设我们点击“熊猫”链接。然后，URL 地址栏更新为包含激活的路线:`htttp://localhost:4200/pandas`。

`Router`检测地址栏的变化，并依次检查路由配置路径列表是否匹配。

```
RouterModule.forRoot([
  {
    path: '', redirectTo: 'home', pathMatch: 'full'
  },
  {
    path: 'home',  component: HomeComponent
  },
  {
    path: 'pandas', component: PandaListComponent
  },
  {
    path: 'pandas/:id', component: PandaDisplayComponent
  }
]);
```

它选择找到的第一个匹配项，然后加载指定的组件。`Router`寻找`RouterOutlet`指令，该指令指定将被识别的组件放在哪里。

最后，它在由`RouterOutlet`定义的位置显示该视图。

# 路线参数

Angular 提供了三种不同类型的管线参数:必需参数、可选参数和查询参数。

## 必需的参数

顾名思义，这些参数是下一个布线元件正常工作所必需的。

必需的参数必须定义为路由配置的一部分。

```
{
  path: 'pandas/:id', component: PandaDisplayComponent
}
```

在前面的代码片段中，我们定义了一个必需的参数——panda 的`id`。导航到该路线需要`id`，因此被路由的组件`PandaDisplayComponent`可以加载并显示所选的熊猫。

为了激活带有所需参数的路径，我们使用`routerLink`并将指定的参数作为额外的元素传递给关联的数组。

```
<div *ngFor="let panda of pandas">
  <a [routerLink]="['/pandas', panda.id]"> {{ panda.name }} </a>
</div>
```

为了以编程方式导航，我们将以类似的方式将参数传递给`Router`的 navigate 方法。

```
constructor(private router: Router) { }

displayPanda(id: number) {
  this.router.navigate(['/pandas', id]);
}
```

最终的 URL 应该是这样的:`http://localhost/pandas/1`。

然后，路由组件可以从`[ActivatedRoute](https://angular.io/api/router/ActivatedRoute)`中读取该参数，并使用它来显示正确的熊猫。

```
 constructor(private route: ActivatedRoute, 
  private pandaService: PandaService) { }

ngOnInit(): void {
  const param = this.route.snapshot.paramMap.get('id');
  if (param) {
    const id = +param;
    this.panda = this.pandaService.getPandaById(id);
  }
}
```

注意，getter 中传递的参数名必须与路径中定义的名称相匹配。

在这里，我们正在导航到一条新的路线。因此，我们简单地使用`paramMap`属性静态地获取一个值。如果我们停留在同一条路线上，但想听参数变化，我们需要订阅`paramMap`观测值。

```
ngOnInit(): void {
  this.route.paramMap.pipe(
    map((paramMap: ParamMap) => +(paramMap?.get('id') ?? -1)),
    map((id: number) => this.pandaService.getPandaById(id))
  ).subscribe((panda: Panda | undefined) => (this.panda = panda));
}
```

## 可选参数

与必需参数不同，可选参数不是强制性的。因此，它们不是路由配置的一部分。

相反，我们将可选参数指定为对象的属性，并在激活路由时将其作为额外的元素传递给关联的数组。

```
<a  [routerLink]="['/pandas', { filterTerm, sortBy }]"> Pandas </a>
```

前面的代码片段传递了一个名为`filterTerm`的可选参数。

> **提示:**我们本来可以把这个写成`{ filterTerm: filterTerm }`，但是这是多余的。我们猜测你已经知道了。

为了以编程方式导航，我们将类似地传递参数。

```
this.router.navigate(['/pandas', { filterTerm, sortBy }]);
```

可选参数被指定为关联数组的单个元素中的一组键和值对。产生的 URL 如下所示:`http://localhost:4200/pandas;filterTerm=Bobo;sortBy=name`。

这可能看起来有点奇怪，但它基本上是用分号分隔的键值对。

这个 URL 是可加书签的，这意味着如果我们将它复制粘贴到地址栏，组件将加载特定的过滤和排序。

然后，布线元件可以读取并使用这些参数。

```
export class PandaDisplayComponent implement OnInit {

  constructor(private route: ActivatedRoute) { }

  ngOnInit(): void {
    const filterTerm = this.route.snapshot.paramMap.get('filterTerm');
    const sortBy = this.route.snapshot.paramMap.get('sortBy');
  }
}
```

同样，如果我们想要监听变化，我们必须订阅`paramMap` observable。

```
ngOnInit(): void {
  this.route.paramMap.subscribe((paramMap: ParamMap) => {
    this.filterTerm = paramMap.get('filterTerm');
    this.sortBy = paramMap.get('sortBy');
  })
}
```

## 查询参数

与可选参数一样，查询参数不作为路由配置的一部分指定。

相反，我们在激活路由时用一个额外的指令`queryParams`来指定它们。

```
<a [routerLink]="['/pandas']" 
   [queryParams]="{ filterTerm, sortBy }"> Pandas </a>
```

为了以编程方式导航，我们将参数作为带有`queryParams`属性的额外导航对象来传递。**注意，这次对象不在关联数组中！**

```
this.router.navigate(['/pandas'], { queryParams: { filterTerm, sortBy } });
```

结果 URL 是`http://localhost:4200?filterTerm=Bobo&sortBy=name`，并且遵循查询参数的标准 URL 格式。同样，这个 URL 是可添加书签的——就像可选参数一样。

然后，布线元件可以读取并使用这些参数。

```
constructor(private route: ActivatedRoute) { }

ngOnInit(): void {
  const filterTerm = this.route.snapshot.queryParamMap.get('filterTerm');
  const sortBy = this.route.snapshot.queryParamMap.get('sortBy');  
}
```

请注意，我们现在使用`queryParamMap`而不是`paramMap`。

相应地，如果我们想要监听变化，我们将不得不订阅`queryParamMap` observable。

```
ngOnInit(): void {
  this.route.queryParamMap.subscribe((paramMap: ParamMap) => {
    this.filterTerm = paramMap.get('filterTerm');
    this.sortBy = paramMap.get('sortBy');
  });
}
```

你可以在下面的 StackBlitz 找到一个工作演示。别忘了[订阅我的简讯](https://vkagklis.medium.com/subscribe)获取更多类似的内容！

## 可选与查询

此时，您一定想知道——可选参数和查询参数之间有什么区别？语法和产生的 URL？

当然，查询参数有一个更熟悉的 URL，但是除此之外，它们还提供了什么额外的东西吗？你打赌！

对于可选参数，如果我们导航回先前的路线，而不将它们传回，则参数将会消失。

另一方面，使用查询参数，我们可以设置`queryParamsHandling`，它们将被自动包含！

```
<button [routerLink]="['/pandas']" 
  queryParamsHandling="preserve"> Back </button>
```

# 结论

在本文中，我们简要了解了路由工作的基本原理。

然后我们研究了 Angular 提供的三种类型的路由参数:必需的、可选的和查询的。

最后，我们介绍了可选参数和查询参数之间的主要区别。

感谢您的阅读！我希望你学到了新的东西。

打算加入 Medium？会员费为 5 美元/月，可以无限制地阅读媒体上的所有报道。使用我的推荐链接:

[](https://kagklis.medium.com/membership) [## 通过我的推荐链接加入 Medium—kakk lis Vasileios

### 阅读 Kagklis Vasileios(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接…

kagklis.medium.com](https://kagklis.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*