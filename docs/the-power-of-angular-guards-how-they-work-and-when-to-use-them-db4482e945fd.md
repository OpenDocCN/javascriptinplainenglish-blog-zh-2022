# 角形防护装置的威力:它们如何工作以及何时使用

> 原文：<https://javascript.plainenglish.io/the-power-of-angular-guards-how-they-work-and-when-to-use-them-db4482e945fd?source=collection_archive---------7----------------------->

![](img/6473f5438b7370275f42aed42c3b20f9.png)

Photo by [Ember Navarro](https://unsplash.com/@ember_?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/guards?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当涉及到限制用户访问您的应用程序中的路线时，角度防护是一个强有力的工具。它们可用于保护敏感路由、阻止非法访问和实现自定义逻辑，因为它们允许您指定用户访问特定路由时必须满足的要求。

在本文中，我们将研究角度防护装置的基本原理及其操作。此外，我们还将介绍各种防护配置，以及在您的应用中何时适合使用它们。到本文结束时，您应该对如何在您的应用程序中利用角度防护来限制对路线的访问有了一个坚实的理解。

导航到某条路由之前路由器调用的功能称为角度防护。基于多个变量，如身份验证状态、权限或自定义逻辑，它们可用于决定是否允许用户访问路径。

在角度应用中，**防护装置**可能在下列情况下**有用**:

1.  **执行异步任务**:在路由启动之前，可以使用解析器保护执行异步操作，例如从服务器下载数据。这可以帮助您的应用程序更有效地运行，确保在触发路线时准备好显示数据。
2.  **保护敏感路由:** Guards 可以用来阻止未经授权的用户访问您的应用程序中的敏感路由，从而保护它们。例如，您可以雇用一名警卫来保证只有授权用户才能访问显示私人数据的路由。
3.  **阻止用户离开组件:**组件防护可用于禁止用户离开组件，除非满足许多条件，如保存对表单的更改。通过这样做，用户可以确保在浏览组件时不会丢失重要信息。
4.  **实现定制逻辑:** Guards 可用于提供定制逻辑，在您的应用程序中控制用户对路由的访问。例如，为了确保用户仅在满足特定要求的情况下才可以访问某个路由，例如拥有一定程度的权限或成员身份，您可以雇用一名警卫。

在 Angular 应用程序中，警卫是管理路由访问和实现自定义逻辑的有用工具。通过允许您指定用户在访问路径之前必须满足的要求，它们可以帮助您提高服务的安全性和有用性。

路线防护罩、组件防护罩和分解器防护罩是**角度防护罩**的三个基本**类别**。

1.  **路由守卫**:当用户试图前往某条路由时，路由器调用路由守卫的例程。它们可以通过返回一个布尔值或一个解析为布尔值的承诺来指示是否应该允许用户访问路径。
2.  **组件防护**:当用户试图激活一个组件时，路由器调用的函数称为组件防护。它们可用于在启用组件之前执行任务，或者阻止组件被实例化。
3.  **解析器保护:**当用户试图行进到一个路由时，路由器调用解析器保护功能。在启用路由之前，它可用于解析路由的数据，使用户能够在路由被激活时查看数据。

**角度防护装置**可在您的应用中以多种不同方式**配置**:

1.  **CanActivate** :一个被称为 CanActivate 的路由保护用于决定是否允许用户激活一个路由。它可用于添加自定义逻辑来管理对路由的访问，或阻止未经授权的用户访问敏感路由。
2.  **CanActivateChild** :一个名为 CanActivateChild 的路由保护用于决定是否允许用户激活子路由。为了管理对嵌套路由的访问，它可以与 CanActivate 结合使用。
3.  **CanDeactivate** :用来评估用户是否可以去激活一个组件的组件保护称为 CanDeactivate。它可以用来阻止用户在满足特定条件之前离开组件，例如保存对表单的更改。
4.  **解析**:路由启动前，使用解析器保护解析路由数据。在路由激活之前，它可能用于从服务器加载数据或执行其他异步操作。
5.  CanLoad :一个被称为 CanLoad 的路由保护被用来决定一个用户是否被允许加载一个组件。

这些只是 Angular 提供的各种防护设置的几个例子。通过利用这些保护和路由配置对象，可以限制对路由的访问，并在应用程序中实现自定义逻辑。

下面是一个在角度应用中如何使用路线防护的示例:

```
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';
import { AuthService } from './auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(
  private authService: AuthService, 
  private router: Router
) {}

  canActivate(): boolean {
    if (this.authService.isAuthenticated()) {
      return true;
    } else {
      this.router.navigate(['/login']);
      return false;
    }
  }
}
```

如果用户通过了身份验证，路由守卫会使用`AuthService`验证他们的身份验证状态，并授予他们访问路由的权限。如果用户未被授权，门卫禁止用户访问该路线，而是将他们引向`login`页面。

必须将此保护添加到要保护的路由的路由配置对象中，以便使用:

```
const routes: Routes = [
  {
    path: 'admin',
    component: AdminComponent,
    canActivate: [AuthGuard]
  }
];
```

现在，每当用户试图访问`/admin`路线时，就会调用`AuthGuard`来确定用户是否应该被允许这样做。如果用户成功通过身份验证，将允许用户访问该路线。如果未通过身份验证，它们将被路由到登录页面。

## 结论:

Angular guards 使您能够限制对路线的访问并实现自定义逻辑，使它们成为增强应用程序安全性和功能的有用工具。通过了解如何在您的应用程序中使用和配置卫士，您可以充分利用卫士的功能来改善用户体验，并确保您的应用程序稳定可靠。

我希望这篇文章对你有所帮助。 ***感谢阅读。***

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **

## **想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。**