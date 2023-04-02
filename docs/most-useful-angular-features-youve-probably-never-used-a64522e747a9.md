# 你可能从未用过的最有用的角度特征

> 原文：<https://javascript.plainenglish.io/most-useful-angular-features-youve-probably-never-used-a64522e747a9?source=collection_archive---------0----------------------->

## 在本文中，我们将重点介绍一些你可能从未听说过的最有用的角度特征。

![](img/d05a45a8882bb2939f79c6bfd431d5ce.png)

Angular 是最好的现代 web 开发人员平台之一，它允许您跨平台开发，重用您的代码，通过使用 Web Workers 和服务器端呈现获得尽可能快的速度，并通过在 RxJS、Immutable.js 上构建数据模型以及使用简单的声明性模板快速创建功能，让您更好地控制可伸缩性。

如果你花了相当多的时间[构建角度应用](https://angular.io/tutorial/toh-pt0)，你可能知道它是如何工作的。但是如果我们告诉你这些角度特征有更多的含义，而你可能已经错过了呢？

让我们弄清楚这是怎么回事！

## **1。标题**

title 标签是一个 HTML 元素，表示网页的标题是什么。标题标签在搜索引擎结果页面上显示为搜索结果的可点击标题。它们对于可用性、SEO 和社交媒体上的分享都很重要。

Angular 应用程序从 index.html 文件中的*标题>…/标题>* 标签获取浏览器窗口的标题。在 Angular 中，当您移动到一个组件时，标题不会改变。

***你知道组件可以改变浏览器的标题吗？***

在@angular/platform-browser 中，有一个服务叫 Title for Angular。我们只是给我们的组件标题服务，并使用 *setTitle* 方法来更改标题。

```
import { Title } from “@angular/platform-browser”@Component({ 
 … 
 }) 
 export class LoginComponent implements OnInit { 
 constructor(private title: Title) {} ngOnInit() { 
 title.setTitle(“Login”) 
 } 
 }
```

当我们转到 LoginComponent 时，“Login”将被设置为浏览器的标题。

我们可以对项目的所有组件都这样做，这样当组件被导航时，组件的标题就会出现在浏览器窗口中。

## **2。元**

我们的 Angular 应用程序显示的大部分内容来自 index.html 文件。我们的应用程序将在 index.html 文件中设置元标签。angular 中的@angular/platform-browser 有一个元服务，允许我们从组件中设置元标签。

这对 SEO 和在社交媒体上分享组件持有的页面非常有帮助。

元元素给出了关于网页的信息，搜索引擎可以使用这些信息来帮助将网页放在正确的类别中。

非常好用；只需从@angular/platform-browser 导入 Meta，并将其注入到我们的组件中。

```
import { Meta } from “@angular/platform-browser”@Component({ 
 … 
}) 
export class BlogComponent implements OnInit { 
 constructor(private meta: Meta) {} ngOnInit() { 
 meta.updateTag({name: “title”, content: “”}) 
 meta.updateTag({name: “description”, content: “Lorem ipsum dolor”}) 
 meta.updateTag({name: “image”, content: “./assets/blog-image.jpg”}) 
 meta.updateTag({name: “site”, content: “My Site”}) 
 } 
}
```

有了这个，我们的博客组件可以在脸书、推特等网站上展示。，带有标题、图片和功能描述。

你也听过这个吗？

## **3。覆盖模板插值**

我们都在模板中使用默认的模板插值器来显示组件中的属性。

开始是，结束是。如果我们在它们之间放置一个属性成员，它将显示在浏览器的 DOM 上。你知道我们可以用自己的符号代替默认符号来表示封装的开始和结束吗？很容易；只要在插值属性中告诉组件装饰器。

```
@Component({ 
 interpolation: [“((“,”))”] 
}) 
export class AppComponent {}In the AppComponent’s template, “” will no longer be used as an interpolation. Instead, “(())” will be used.@Component({ 
 template: ` 
 <div> 
 ((data)) 
 </div> 
 `, 
 interpolation: [“((“,”))”] 
 }) 
 export class AppComponent { 
 data: any = “dataVar” 
 }
```

页面渲染时将显示*【数据变量】*而不是*“((数据)”)*。

## **4。位置**

使用定位服务，我们可以找到我们正在看的窗口的 URL。根据使用的 LocationStrategy，Location 将遵循 URL 的路径或散列段。

有了位置，我们可以转到一个 URL，在平台的历史中前进，在平台的历史中后退，更改浏览器的 URL，并替换平台历史堆栈中的顶部项目。

我们通过从 CommonModule 注入位置服务来使用它。

```
import { Location } from “@angular/common”@Component({ 
 … 
}) 
export class AppComponent { 
 constructor(private location: Location) {} navigateTo(url) { 
 this.location.go(url) 
 } goBack() { 
 location.back() 
 } goForward() { 
 location.forward() 
 } 
}
```

## **5。文件**

有时候，我们希望获得文档模型，以便我们的 Angular app 可以进行 DOM 操作。

这是文件给出的内容。文档是阿迪令牌，代表呈现的主上下文。这就是浏览器的 DOM 文档。它提供了适用于任何环境的 DOM 操作。

**注意:**如果应用程序上下文和呈现上下文不同，文档可能在应用程序上下文中不可用(例如，当在 Web Worker 中运行应用程序时)。

假设我们的 HTML 有这个元素:

```
<canvas id=”canvas”></canvas>We can get the canvas HTMLElement by putting DOCUMENT: in front of it.@Component({}) 
export class CanvasElement { 
 constructor(@Inject(DOCUMENT) _doc: Document) {} 
}
```

然后，我们可以通过调用 getElementById()来获取 canvas 的 HTMLElement

```
@Component({}) 

export class CanvasElement { 

 constructor(@Inject(DOCUMENT) _doc: Document) {} renderCanvas() { 

 this._doc.getElementById(“canvas”) 

 } 

}
```

我们可以使用 ElementRef 和模板引用安全地做到这一点，但是你明白了。

***注意:*** *小心脚下！直接与 DOM 交互是有风险的，可能会导致 XSS 风险。*

## **6。属性装饰器**

组件、模块和指令装饰器是我们在 Angular 应用中使用最多的。

我们有这个属性修饰器，它允许我们传递一个静态字符串，而不会因为不检查它是否改变而减慢速度。

attribute decorator 的值只被检查一次，不会再被检查。它们的用法与@Input 相同:

```
@Component({ 
 … 
 }) 
 export class BlogComponent { 
 constructor(@Attribute(“type”) private type: string ) {} 
 }
```

## **7。http 接收器**

这是 Angular 非常强大的一部分。它的工作方式很像美国的拦截战斗机。它停止 HttpRequests 并处理它们。

通过调用*next . handle(transformed req)*，大多数拦截器在将请求发送给链中的下一个拦截器之前，都会更改发出的请求。

句柄(transformedReq)。

在极少数情况下，拦截器可能希望自己处理一个请求，而不是将它传递给整个链。这种行为没问题。

HttpInterceptor 可用于:

*   证明
*   缓存，
*   假后端
*   更改 URL
*   更改标题

它很容易使用。首先，创建一个服务并实现 HttpInterceptor 接口。

```
@Injectable() 
export class MockBackendInterceptor implements HttpInterceptor { 
 constructor() {} intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> { 
 … 
 } 
}
```

之后，将其添加到您的主模块中:

```
@NgModule({ 
 …providers: [ 
 { 
 provide: HTTP_INTERCEPTORS, 
 useClass: MockBackendInterceptor, 
 multi: true 
 } 
 ] 
 … 
 }) 
 export class AppModule {}
```

## **8。AppInitializer**

有时候，我们希望在 Angular 应用程序启动时运行一段代码。例如，我们可能想要加载一些设置、缓存、配置或签入。AppInitializer 标记使这变得更容易。

APP INITIALIZER 是第一次启动应用程序时运行的函数。

用起来很简单。假设我们希望我们的 Angular 应用程序在启动时运行这个 *runSettings* 函数:

```
function runSettingsOnInit() { 
 … 
 }
```

我们将它添加到主模块 AppModule 的 NgModule 装饰器中，位于提供者部分:

```
@NgModule({ 
 providers: [ 
 { provide: APP_INITIALIZER, useFactory: runSettingsOnInit } 
 ] 
 })
```

## **结论**

今天，我们希望你对 [Angular app 开发](https://jumpgrowth.com/angular-js-development/)有了一些新的认识。如果不是，那么不要担心；我们在知识上都有差距，上面的列表并不完整。棱角很大，很复杂。查看角源，看看是否能找到以前从未被写过或听说过的特征。我会等着看你发现什么。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***