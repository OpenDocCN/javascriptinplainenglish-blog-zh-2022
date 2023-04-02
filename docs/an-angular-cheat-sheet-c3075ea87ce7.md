# 给初学者的有角度的小抄

> 原文：<https://javascript.plainenglish.io/an-angular-cheat-sheet-c3075ea87ce7?source=collection_archive---------8----------------------->

## Angular 中核心概念的简要教程

![](img/d9936919054373200361b2b0d6a5edf2.png)

ffImage created by the author | Original logo credits: [angular.io](https://angular.io/presskit)

Angular 是 Google 开发的一个基于类型脚本的框架，用于开发基于 web 和移动的应用程序。在本文中，我们将介绍 Angular 中的一些核心概念，比如 Angular CLI、Decorators、生命周期挂钩、模板语法和路由。

## 角度 CLI

Angular 为你提供了一个内置的**命令行界面**，使得设置和运行你的应用程序变得非常容易和快速。要安装它，您需要安装节点软件包管理器。

`**npm install -g @angular/cli**` **:** 该命令帮助您使用 npm 下载并安装最新的 Angular CLI。一旦安装了 Angular CLI，您可以通过`ng`命令使用它。

`**ng help**` **:** 您可以使用该命令查看所有可用的命令及其用法。您还可以使用`ng command-name — help`查看任何特定命令的用法和选项

`**ng doc keyword [options]**` **:** 该命令将在浏览器上打开官方 angular 文档，并搜索您提供的关键字。

`**ng new app-name [options]**` **:** 该命令允许您创建并初始化一个新的 angular 应用程序，让您开始开发。

`**ng add package-name [options]**` **:** 您可以使用此命令将发布的 npm 包添加到您的工作区，并配置项目以使用添加的库。

`**ng generate schematic-name [options]**` **:** 该命令帮助您根据您提供的原理图，在当前工作空间中生成/修改项目文件。几种最常用的原理图是`application, module, class, component, service, directive,`和`pipe`。你可以在这里找到所有你能用到的原理图[。](https://angular.io/cli/generate#schematic-commands)

`**ng serve project-name [options]**` **:** 该命令允许您在当前工作区中构建并运行指定的项目。执行此指令时，您在项目中所做的任何变更都会自动重建并反映在浏览器中。你也可以使用`--open or -o`选项直接在浏览器上打开构建的项目，你也可以添加`--ssl`选项来使用 HTTPS 运行它。

`**ng build project-name [options]**` **:** 该命令构建指定的项目，并将输出文件生成到`/dist`目录中。这个目录的内容可以在以后使用您想要的 web 服务器来运行您的应用程序。

## 装修工

angular 中的 decorator 是一个函数，我们用它将元数据附加到一个**类、方法、访问器、属性或参数**上。我们使用`@`符号加上装饰者的名字来应用装饰者。在这一节中，我们将讨论不同类型的装饰者。

**@NgModule**

Angular 模块是一个由`@NgModule` decorator 标记的类，它帮助配置和组织相关的东西。它采用一个元数据对象来标识模块自己的组件、指令和管道，您还可以向应用程序添加服务提供者。我们可以通过`exports`属性公开一些，以便其他外部组件可以使用它们。

```
@NgModule({
  declarations: [ AppComponent ],
  imports: [ BrowserModule ],
  exports: [ AppComponent ],
  providers: [ AppService ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

**声明**键是作为该模块一部分的组件、指令和管道的列表。

**imports** 键是要导入该模块的模块列表。

**exports** 键是导入该模块的外部模块可见的组件、指令和管道的列表。

**providers** 键是依赖注入提供者的列表。这些对于该模块的内容和该模块的导入者都是可见的。

**@组件**

`@Component` 声明一个类是一个组件。它提供关于组件的元数据，如要链接的模板、要链接的样式、选择器名称、动画、要使用的提供者、输入、输出等。,

```
**@Component**({
  selector: 'demo',
  templateUrl: './demo.component.html',
  styleUrls: ['./demo.component.scss']
})
export class DemoComponent implements OnInit { }
```

**@指令**

`@Directive`表示一个类是一个指令。Angular 中使用指令来处理模板中不同元素的行为和结构。您可以看到一个内置结构指令的例子，它根据条件决定是否将演示组件的模板添加到 DOM 中。

```
<demo ***ngIf** = "showDemo"/>
```

另一种类型的指令是行为指令，它决定了组件在模板中的外观或行为，如下所示。

```
<demo [ngClass]="demoClasses"/><demo [ngStyle]="demoStyles"/>
```

**@可注射**

`@Injectable`声明一个类是提供者。然后，该类可以作为提供者注入到其他组件中。

```
**@Injectable**({
  providedIn: 'root'
})
export class DemoService { ... }
```

这里的元数据`provideIn: ‘root’`意味着应用程序中的所有组件都可以使用该服务。

通过将该服务添加到构造函数中，您可以在其他组件中注入和使用该服务，如下所示。

```
constructor(demoService: DemoService)
```

**@输入@输出**

`@Input`和`@Output`装饰器用于声明可用于组件间通信的属性。`@Input`用于将属性绑定到外部组件。

```
Template of first component: <demo [myInput]="expression">Second component: @Input() myInput: string;
```

`@Output`用于将事件绑定到外部组件。

```
Template of first component: <demo (myEvent)="eventName('hello')">Second component: 
@Output() myEvent = new EventEmitter();
myEventName(value: string) {     
  this.myEvent.emit(value);   
}
```

我们将在模板语法部分更详细地讨论输入和输出装饰器。

**@管道**

`@Pipe`装饰器用于将一个类声明为管道。它用于使用角度模板中的内置管道或自定义管道来转换数据。任何管道类都必须实现一个`PipeTransform`接口，表达式被传递给`transform()`。该方法处理如何转换给定表达式的逻辑。你可以在下面看到一个内置管道的例子。

```
{{ demoExpression | uppercase }}
```

## 生命周期挂钩

组件/指令实例的生命周期始于 angular 实例化该实例并呈现该组件的视图及其子视图。生命周期经历初始化、属性值变化的变化检测以及视图和组件实例的更新，并在 Angular 销毁实例并从 DOM 中删除渲染模板时结束。

*   `**ngOnChanges**` **:** 这是 angular 为实例设置或重置属性时，在生命周期中触发的第一个挂钩。
*   `**ngOnInit**` **:** 当 Angular 在第一次设置并显示绑定的输入属性后初始化组件/指令时，调用这个函数。
*   `**ngDoCheck**` **:** 当您需要检测变化并采取行动时触发。
*   `**ngAfterContentInit**` **:** 当 Angular 将内容推入组件的视图，或者使用了指令的视图时，调用这个函数。
*   `**ngAfterViewInit**` **:** 当 Angular 完成初始化组件的视图和子视图，或者包含指令的视图时，调用这个函数。
*   `**ngOnDestroy**` **:** 在 Angular 破坏组件/指令之前触发。这个钩子可以用于最终的数据清理，取消订阅任何可观察到的数据，并分离事件处理程序以避免内存泄漏。

## 模板语法

## 插入文字

插值允许您将表达式嵌入到模板的标记文本中。它使用双花括号`{{`和`}}`作为分隔符。

下面显示了一个使用插值嵌入模板的表达式示例。

```
// variables in the componentcurrentUser = 'George'
currentProfile = 'assets/defaultIcon.png';// template using interpolation<h2> Current User: {{currentUser}} </h2>
<div><img alt="item" src="{{currentProfile}}"></div>
```

这里 angular 用相应组件属性的字符串值替换了`currentUser`和`currentProfile`变量。在这种情况下，值将是`George`和`assets/defaultIcon.png.`

## 模板语句

模板语句是您可以在模板中用来响应用户事件的属性或方法。您可以使用它们来显示动态内容或捕捉用户操作。

模板语句出现在等号`=`字符右边的引号中，就像`(event)="statement"`一样。下面的示例展示了如何在模板中使用它。

```
<button type="button" (click)="deleteUser()">Delete User</button>
```

模板语句解析器既支持基本赋值(`=`)，也支持在引号内用分号(`;`)链接表达式。

## 有约束力的

数据绑定根据组件的状态保持模板最新。您可以绑定一堆东西，如属性、类、特性、样式和事件，还可以用两种方式绑定数据。您可以在下面看到一些数据绑定的例子。

```
// property
<img [alt]="user.name" [src]="userImageUrl">// event
<button type="button" (click)="onSave()">Save</button>// two way
<input [([ngModel](https://angular.io/api/forms/NgModel))]="name">// attribute
<button type="button" [attr.aria-label]="help">help</button>// class
<div [class.special]="isSpecial">Special</div>// style
<button type="button" [style.color]="isSpecial ? 'red' : 'green'">
```

## 指令

指令用于修改模板中不同元素的行为和结构。从广义上讲，有两种指令，属性指令和结构指令。

**属性指令**

这些类型的指令通过改变元素的属性和特性来决定元素的行为。您可以在下面看到不同属性指令的例子。

```
<div [ngClass]="isSpecial ? 'special' : ''">
  This div is special
</div>
```

在这个例子中，我们使用`ngClass`指令根据标志的结果给 div 分配一个类。

```
// template
<div [ngStyle]="currentStyles">   
  This div is italic, normal weight, and extra large (24px). 
</div>
// component content
currentStyles: Record<string, string> = {};this.currentStyles = {     
  'font-style': 'italic',
  'font-weight': 'normal',     
  'font-size': '24px'     
};
```

这里，我们通过使用`ngStyle`指令传递多个 CSS 规则的记录，将一组样式应用于 div。

```
<label for="example-ngModel">[([ngModel](https://angular.io/api/forms/NgModel))]:</label> 
<input [([ngModel](https://angular.io/api/forms/NgModel))]="currentItem.name" id="example-ngModel">
<input [[ngModel](https://angular.io/api/forms/NgModel)]="currentItem.name (ngModelChange)="setUppercaseName($event)" id="example-uppercase">
```

这里我们使用双向绑定的`ngModel`指令来显示其他输入字段中的相同变量，因此它们的值都是最新的。

**结构指令**

这些类型的指令根据传递给它们的表达式决定模板的结构。你可以在下面看到一些例子。

```
<app-item-detail *ngIf="show" [item]="item"></app-item-detail>
```

根据`show`标志的结果，`*ngIf`指令可用于显示或隐藏模板中的 app-item-detail 组件。

```
<div *ngFor="let item of items">{{item.name}}</div>
```

`*ngFor`指令用于遍历数据列表，并根据列表中值的数量创建模板。在这里，对于每一项，我们用该项的名称创建一个新的 div。

```
<div [ngSwitch]="currentItem.feature">   
  <app-stout *ngSwitchCase="'stout'" [item]="currentItem"/>           

  <app-slim *ngSwitchCase="'slim'" [item]="currentItem"/>   

  <app-bright *ngSwitchCase="'bright'" [item]="currentItem"/> <app-unknown *ngSwitchDefault [item]="currentItem"/>
</div>
```

在这里,`*ngSwitch`指令用于根据项目特性的值决定在模板中显示哪个组件。

## 输入和输出装饰器

在我们需要在父组件和一个或多个子组件之间共享数据的场景中，`@Input`和`@Output`装饰器开始发挥作用。

**输入**

为了将数据从父组件传递到子组件，我们使用了`@Input`装饰器。你可以在下面的例子中看到它是如何工作的。

```
// child component
export class UserDetailsComponent {   
   @Input() username = ''; // decorate the property with @[Input](https://angular.io/api/core/Input)() 
}// child template
<p> Logged in user: {{username}} </p>
```

这里你可以看到我们用`@Input`装饰器装饰了允许数据从父组件流入子组件的属性。

```
// parent component template 
<h2>Parent Component</h2>
<user-detail [username]="currentUser"></app-item-detail>// parent component
export class ParentComponent {   
  currentUser = 'George'; 
}
```

在父组件中，您可以看到我们在模板中使用了子组件的装饰器，并将父组件中的变量`currentUser`绑定到子组件的已配置的`username`属性..

**输出**

另一方面，为了将数据从子组件传递到父组件，我们使用了`@Output` 装饰器。你可以在下面的例子中看到它是如何工作的。

```
// child component
export class UserDetailComponent {    
  @Output() newUserEvent = new EventEmitter<string>();
  addNewUser(value: string) { 
    this.newUserEvent.emit(value);   
  } 
}// child component's template
Add user:<input type="text" id="user-input" #newUser> 
<button type="button" (click)="addNewUser(newUser.value)">
  Add to parent's list
</button>
```

您可以在这里看到，我们已经将`@Output`装饰器与 click 事件绑定，以触发一个采用单参数方法的事件。

```
// parent component
export class ParentComponent {   
  users = ['user1'];    
  addUser(newUser: string) {     
    this.users.push(newUser);   
  }
}// parent component's template
<user-details (newUserEvent)="addUser($event)"></user-details>
```

您可以看到，我们为子组件映射的事件可以用来触发父类的`addUser()`。它将子模板中配置的事件数据从输入字段传递到父组件的`users`列表中

## 管道

如果您想要解析或转换表达式的值，可以在模板中使用管道。您可以只使用属性名，后跟`|`，然后是您想要使用的管道名。模板上可见的最终输出将基于对传递的表达式执行的转换。

```
<p>The user's birthday is {{ birthday | date }}</p>
```

## 按指定路线发送

角度路由使您能够在应用程序的不同页面之间导航。要在您的应用程序中使用路由，请使用类似`ng new app-name --routing`的附加选项创建您的 angular 应用程序。它将生成一个 approving module，并在 approving module 中创建一个路由数组。您可以在此阵列中为您的应用程序添加路由，如下所示。

```
const routes: Routes = [   
  { path: 'component-one', component: FirstComponent },   
  { path: 'component-two', component: SecondComponent }, 
];
```

现在，您可以使用 routerLink 属性在视图中访问这些不同的页面。但是首先，你需要添加`<router-outlet></router-outlet>`到你的模板中，这是导航页面在应用视图中显示的地方。您可以在下面看到一个示例模板，它使用了上面配置的路由。

```
<ul>
  <li>
    <a routerLink="/component-one" routerLinkActive="active">
      First Page
    </a>
  </li>     
  <li>
    <a routerLink="/component-two" routerLinkActive="active">
      Second Page
    </a>
  </li>   
</ul><router-outlet></router-outlet>
```

`routerLinkActive="active"`将在链接激活时添加一个激活类。

您还可以从组件导航到不同的路线。您需要将路由器导入并注入到您的组件中，如图所示。

```
constructor( private router: Router ) {}
```

您可以稍后在您所需的方法中执行以下操作来导航到所需的路线。

```
this.router.navigate([‘/component-one’, { id: 1 }]);
```

> **注意:**配置路由的顺序很重要，因为路由采用先匹配后获胜的策略，所以请确保首先提及最具体的路由，然后提及不太具体的路由，最后提及与默认路由匹配的空路由。

## 从路线中获取信息

您需要导入`ActivatedRoute`和`ParamMap`并将`ActivatedRoute`注入到您想要读取信息的组件中，如下所示。

```
constructor( private route: ActivatedRoute, ) {}
```

您可以更新组件中的`ngOnInit()`方法来访问`ActivatedRoute`并跟踪您想要的参数，如图所示。

```
ngOnInit() {
  /** 
   To access required and optional parameters specific to a route 
   eg: user/:paramOne  
  */
  this.route.paramMap.subscribe(params => {     
    this.myParameter = params.get('paramOne');   
  }); /** 
   To access query parameters which are available to all routes 
   eg: user/one?id=1  
  */
  this.route.queryParams.subscribe(params => {     
    this.myParameter = params['id'];   
  });
}
```

## 使用警卫认证路线

你可以使用`ng generate guard custom-guard`为我们的路线生成一个守卫。然后，您可以使用`canActivate`方法来定制认证逻辑，如图所示。

```
export class CustomGuard implements CanActivate {   
  canActivate( 
     next: ActivatedRouteSnapshot, 
     state: RouterStateSnapshot) : boolean {       
        // custom authentication logic here 
  } 
}
```

创建守卫后，您可以将它用于您的路线，如图所示。

```
{   
  path: '/component-one',   
  component: FirstComponent,   
  canActivate: [CustomGuard] 
}
```

这是 Angular 中的一些核心概念，希望你会发现它们有用。

感谢阅读，祝学习愉快！

如果你喜欢阅读这样的故事，并想支持我成为一名作家，可以考虑[注册成为一名媒体会员](https://nehalk.medium.com/membership)。一个月 5 美元，你可以无限制地阅读 Medium 上的所有故事。如果你[用我的链接](https://nehalk.medium.com/membership)注册，我会赚一小笔佣金。

[](https://nehalk.medium.com/membership) [## 通过我的推荐链接加入 Medium-Nehal Khan

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

nehalk.medium.com](https://nehalk.medium.com/membership) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*