# 角度使用类提供者:简单解释

> 原文：<https://javascript.plainenglish.io/angular-useclass-provider-simple-explanation-8ceab2354b60?source=collection_archive---------7----------------------->

## 在 Angular 中，provider 是对[依赖注入](https://angular.io/guide/dependency-injection)系统关于如何获得依赖值的指令。

![](img/86d27380f885d4aaf07b3ab45e6a5bb4.png)

Note: I used the power of Subzero to attract readers.

> `provide`属性持有令牌，该令牌用作定位依赖值和配置注入器的键。第二个属性是一个**提供者定义对象**，它告诉注入器如何创建依赖值。

```
[{ provide: Logger, useClass: Logger }]
```

这看起来很有趣，但是让我们试着去理解它到底提供了什么配置。让我们假设我们有这个具有`log`方法的服务。

我们正在组件中导入我们的服务，并调用`log`方法

输出将是:

```
[Value is]: Hello
```

现在让我们假设我们有另一个服务- `ColorLog`，它做同样的事情:在控制台中记录消息，但是有额外的颜色和另一个前缀。

现在，如果我们想使用新创建的 **ColorLog** 服务，我们可以在构造函数中替换服务注入(糟糕的解决方案)。

```
export class HelloComponent implements OnInit {
 // change instance here
constructor(private logService: ColorLogService)
 {}
 .... 
}
```

但是在组件中改变代码并不是一个好的解决方案，所以这里我们可以使用组件的**提供者数组**。使用`useClass`的整体思想是告诉组件它应该使用哪个类实例。

注意语法

```
{
  provide: LogService,
  useClass: ColorLogService,
}
```

这意味着在我们的组件中，`logService`应该是`ColorLogService`的实例，而不是`LogService`。好了😉。

如果你想只使用服务的一个实例，你可以使用[使用现有的](https://angular.io/guide/dependency-injection-providers#alias-providers-useexisting)而不是`useClass`

检查[堆栈](https://stackblitz.com/edit/a-angular-useclass?devToolsHeight=33&file=src/app/hello.component.ts)上的代码。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****