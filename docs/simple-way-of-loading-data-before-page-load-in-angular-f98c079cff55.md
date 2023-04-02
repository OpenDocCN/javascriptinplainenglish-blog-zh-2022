# Angular 中页面加载前加载数据的简单方法

> 原文：<https://javascript.plainenglish.io/simple-way-of-loading-data-before-page-load-in-angular-f98c079cff55?source=collection_archive---------0----------------------->

![](img/e6b7efce652747532d6a004d36a2a152.png)

Photo by [Mike van den Bos](https://unsplash.com/@mike_van_den_bos) on [Unsplash](https://unsplash.com/photos/jf1EomjlQi0)

您可能已经在 app.component 的 ngOnInit 函数中尝试过这样做，但是意识到您的数据需要更快地加载。您可能也尝试过实现解析器，但是意识到它们更适合于单独的路由环境。这里有另一种在页面加载之前加载数据的方法，你可能还不知道:这个 **APP_INITIALIZER**

## **定义**

在深入研究代码之前，让我们更好地理解 APP_INITIALIZER 是什么以及它是如何工作的。

APP_INITIALIZER 标记允许您为应用程序提供额外的初始化函数。您可能已经从名称中了解到，初始化函数是在应用程序初始化期间执行的。这些函数的返回类型必须是 void、Promise 或 Observable。如果从这些函数中的任何一个返回了一个承诺或一个可观察值，那么应用程序只有在它们完成之后才被初始化。

更简单地说，我喜欢把它看作是定义一个“启动”阶段，在这个阶段，你可以确保在用户开始与它交互之前，你的应用程序正常运行所需的所有核心数据都已加载。

下面是一些可以在初始化函数中加载内容的例子:

*   翻译
*   经过验证的用户数据
*   配置数据

## **举例**

为了简单起见，让我们以加载当前经过身份验证的用户的数据为例。

大多数 web 应用程序在屏幕的右上角显示当前用户的个人资料图片和姓名，所以让我们实现一些类似的东西。我将为 CSS 使用全新的角度安装(14.1)和 Bootstrap 5:

```
ng new angular-app-initializer --routing --style=scss
cd angular-app-initializer
npm install --save bootstrap
```

现在打开您的`styles.scss`并导入引导程序:

```
*// src/styles.scss*@import '~bootstrap/scss/bootstrap';
```

> 如果您使用不同版本的 Angular，一些导入和语法可能会有所不同，所以如果您遵循代码，请注意这一点。

## **奠定基础**

让我们首先创建一个负责提供当前用户数据的服务，现在看起来应该是这样的:

```
*// src/app/service/user.service.ts*import { *Injectable*} from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  private _data: IUserData = {
    name: 'guest',
    avatar: 'assets/no-avatar.png' *// grab a random avatar image and put it in your assets folder*
  }

  get data(): IUserData {
    return this._data;
  }
}

export interface IUserData {
  name: string,
  avatar: string
}
```

这将是我们数据的默认值，直到我们请求获取实际的当前用户数据。

让我们利用这些数据，并将其显示在屏幕的右上角。为了简单起见，我们将直接在 AppComponent 中这样做。

首先，我们注入我们的用户服务:

```
*// src/app/app.component.ts*import { Component } from '@angular/core';
import { UserService } from './service/user.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  constructor(public userService: UserService) {
  }
}
```

然后对于 HTML:

```
*// src/app/app.component.html*<nav class="navbar navbar-light bg-light">
  <div class="container">
    <a class="navbar-brand">MyApp</a>
    <div class="d-flex align-items-center">
      **<p class="mb-0">{{userService.data.name}}</p>
      <img src="{{userService.data.avatar}}"
           class="ms-2 rounded-circle"
           style="width: 60px">**
    </div>
  </div>
</nav>
<main class="container py-4">
  <h1>Dashboard</h1>
  <p>Dashboard content goes here...</p>
</main>
```

我强调了显示用户姓名和个人资料图片的重要部分。

现在我们已经奠定了基础，剩下要做的就是实现一个获取实际用户数据的函数，然后看看我们将在何时何地调用它。

我不打算为此使用实际的后端服务，而是在我们的 assets 文件夹中创建一个 JSON 文件，我们将在这里对数据进行硬编码:

```
*// src/assets/user.json*{
  "name": "Dragos Becsan",
  "avatar": "assets/avatar.jpg" *// grab another avatar image and put it in your assets folder - remove this comment*
}
```

我们将定义负责获取`UserService`中数据的函数，如下所示:

```
*// src/app/service/user.service.ts*import { *Injectable*} from '@angular/core';
**import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
import { delay, tap } from 'rxjs/operators';**

@Injectable({
  providedIn: 'root'
})
export class UserService {
  private _data: IUserData = {
    name: 'guest',
    avatar: 'assets/no-avatar.png'
  };

  **constructor(private http: HttpClient) {
  }

  public loadData(): Observable<IUserData> {
    return this.http.get<IUserData>('./assets/user.json')
    .pipe(
      delay(1000)**, // to mimic an actual HTTP request sent to a backend service
 **tap((response: IUserData) => this._data = response)
    );
  }**

  get data(): IUserData {
    return this._data;
  }
}

export interface IUserData {
  name: string,
  avatar: string
}
```

不要忘记导入`AppModule`中的`HttpClientModule`。

## **实现 APP_INITIALIZER**

正如我们在定义部分学到的，APP_INITIALIZER 让我们定义额外的初始化函数，所以现在让我们在一个单独的文件中定义一个。

```
*// src/app/initializer/app.initializer.ts*import { Observable } from 'rxjs';
import { IUserData, UserService } from '../service/user.service';

export function initializeAppFactory(userService: UserService): () => Observable<IUserData> {
  return () => userService.loadData()
}
```

> 您可以随意命名文件和函数。我通常坚持使用一个更通用的名字，因为我通常使用一个`forkJoin`在一个函数中加载我需要的所有东西。如果你喜欢用不同的方式，你可以，例如，将这个命名为`loadUserDataFactory`或类似的名字(因为这是它唯一做的事情)，然后创建单独的函数来加载你可能需要的任何其他数据。

现在唯一要做的就是将这个函数标记为 APP_INITIALIZER，这样 Angular 就知道在 APP 初始化期间执行它。为此，我们需要将以下提供者添加到 AppModule 中的 **providers** 数组中:

```
*// src/app/app.module.ts*...providers: [
  {
    provide: ***APP_INITIALIZER***,
    useFactory: initializeAppFactory,
    deps: [UserService],
    multi: true
  }
],...
```

仅此而已。如果您现在刷新页面，您应该会看到大约 1 秒钟的空白页面(因为我们在获取 JSON 文件时增加了延迟)，之后页面将加载实际的用户名和头像(在 user.json 文件中指定的那些),显示在右上角。

## **需要考虑的事情**

*   可能需要注意的最重要的事情是，如果从任何初始化函数返回的可观察值出错，应用程序将不再被初始化。在我们的示例中，您可以通过重命名或临时删除`user.json`文件来看到这一点，这将导致 Observable 失败并出现 404 错误。因此，你将停留在最初的空白页上。
    为了防止这种情况发生，请始终确保使用`catchError`操作符捕获任何潜在的错误，并为您的数据提供默认值或将用户重定向到特定的错误页面，在那里您可以为他们提供出错的详细信息以及如何继续前进。在我们的示例中，重定向到一个错误页面可能看起来像这样— *如果您想尝试一下，不要忘记添加* `*Router*` *作为依赖项，方法是在 AppModule 中更新提供者的* `*deps*` *键，并创建新页面及其路由*:

```
*// src/app/initializer/app.initializer.ts*import { from, Observable } from 'rxjs';
import { UserService } from '../service/user.service';
import { catchError } from 'rxjs/operators';
import { Router } from '@angular/router';

export function initializeAppFactory(userService: UserService, router: Router): () => Observable<any> {
  return () => userService.loadData().pipe(
    catchError(() => from(router.navigate(['/error'])))
  );
}
```

*   你看到的 1 秒钟的空白页实际上是`index.html`。发生这种情况的原因是，由于应用程序直到可观察的完成才被初始化，所以`<app-root>`元素没有被填充，所以你看不到任何东西。我通常做的是添加一个加载图像/文本作为`<app-root>`元素的子元素。当应用程序完成初始化时，您放在`<app-root>`中的任何内容都将被覆盖。下面我给你举个例子，你可以试试。如果你想试验一下，可以考虑在 initializeAppFactory 函数中增加可观察对象的延迟。

```
*// src/index.html*...<app-root>
  <div class="vh-100 d-flex align-items-center justify-content-center">
    <p class="h2">Loading...</p>
  </div>
</app-root>...
```

*   习惯使用 RxJS(除非你使用承诺),因为你经常需要使用一堆 RxJS 函数和操作符来获得正确的结果。`forkJoin`、`iif`、`switchMap`、`map`、`catchError`、`tap`是我在这种情况下经常使用的。例如，在我们的例子中，我们只考虑了用户登录的情况，但是如果用户实际上是一个客人呢？在这种情况下，我们可能希望坚持使用我们定义的默认数据。在单个流中实现这一点的一种方法类似于这样— *请记住，这只是一个示例，它在当前项目中不会开箱即用，因为我们还没有一起定义任何*`*authService*`*:*

```
**// src/app/service/user.service.ts*...public loadData(): Observable<IUserData> {
  return iif(
    () => this.authService.isLoggedIn,
    this.http.get<IUserData>('./assets/user.json'),
    of({name: 'guest', avatar: 'assets/no-avatar.png'})
  ).pipe(
    tap((output: IUserData) => this._data = output),
  );
}...*
```

## *资源:*

*[https://angular.io/api/core/APP_INITIALIZER](https://angular.io/api/core/APP_INITIALIZER)T17[https://www.learnrxjs.io/learn-rxjs/operators](https://www.learnrxjs.io/learn-rxjs/operators)*

*非常感谢你一直坚持到最后！🎉*

*如果你觉得这个教程很有用，请点击拍手按钮，跟我来获取更多类似的内容。*

*如果有任何建议，特别是你希望我在我的简历中列出的技术，我都愿意接受，所以如果你有任何意见，请随时发表。*

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。****