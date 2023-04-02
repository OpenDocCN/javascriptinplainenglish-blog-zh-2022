# 角分量通信:6 种方式可供选择

> 原文：<https://javascript.plainenglish.io/angular-component-communication-81e5e02c6cbe?source=collection_archive---------1----------------------->

## 了解 Angular 中数据共享和组件通信的 6 种不同方式。

![](img/191da313887a9cde269350b10ceaa77a.png)

Photo by [Annie Spratt](https://unsplash.com/@anniespratt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

良好的沟通是任何关系成功的关键因素。应用程序中的关系也不例外。应用程序的组件和其他部分需要协同工作才能完成任务。他们需要能够清晰有效地交流。

在本文中，我们将介绍 6 种在 Angular 中实现 ***组件通信的方法:***

1.  使用`@Input`装饰器来定义输入属性并将数据从父节点传递给子节点
2.  使用`@Output`装饰器来定义输出属性，并将响应从子节点发送回父节点
3.  使用`@ViewChild`或`@ViewChildren`装饰器从父组件中设置或读取子组件的属性
4.  使用服务作为中介在应用程序中不相关的组件之间进行通信
5.  使用 NgRx 的存储作为事实的单一来源，从应用程序中不相关的组件创建或读取应用程序状态
6.  使用布线参数将数据从当前元件传递到下一个布线元件

看起来我们有很多要讲的！

所以，让我们开始吧！

# **目录**

```
[1\. The @Input Decorator (Parent-to-Child)](#4219)
[2\. The @Output Decorator (Child-to-Parent)](#f5ed)
[3\. The @ViewChild Decorator](#a09b)
[4\. Service as an Intermediary](#4cfd)
[5\. NgRx](#a3fe)
[6\. Route Parameters](#c877)
[Conclusions](#f185)
```

# 1.@Input Decorator(父到子)

如果两个组件有父子关系，在大多数情况下，使用输入属性是将数据从父组件传递给子组件的最佳选择。

为了定义一个输入属性，我们将`@Input`装饰器添加到属性中。

然后，该属性可用于绑定。父节点可以使用它将值、变量或表达式绑定到输入属性。

输入属性`[checked]`是绑定目标，而`isChecked`是绑定源。由于使用了属性绑定，这意味着如果父节点修改了其端的源属性，子节点将接收到更改后的值。

Angular component communication demo using the @Input() decorator

# 2.@Output Decorator(子到父)

如果子组件需要与父组件进行通信，我们可以在子组件中定义输出属性。但是，与使用属性绑定的输入属性不同，输出属性通过发出事件来工作，这些事件是通过事件绑定来捕获的。

为了定义输出属性，我们将`@Output`装饰器添加到属性中。然后，子组件可以使用该属性发出事件。或者，它可以将一些数据(称为事件负载)附加到发出的事件。

父级可以在她的模板中使用事件绑定来捕获这些事件。

然后它可以调用一个方法来对事件做出反应。

Angular component communication demo using the @Output() decorator

你知道吗？

可以组合`@Input`和`@Output`装饰器来实现父属性和子属性之间的双向绑定。

在子组件类中，我们定义了一个输入和输出属性。输出属性名必须是输入属性名，并以后缀`Change`结尾。

Angular component communication demo using @Input() and @Output() decorators for two-way binding

# 3.@ViewChild 装饰器

不用通过输入属性传递数据或通过输出属性发出事件，父节点可以使用`@ViewChild`或`@ViewChilden`装饰器直接访问子节点的属性和方法。

`@ViewChild`装饰器允许我们获得对模板中任何元素、指令或子组件的引用。

要获得引用，我们可以使用模板引用变量:

或子组件类型:

然后，我们可以使用该引用来访问子组件的属性和方法。但是，这种交流方式有局限性。

首先，在`AfterViewInit`生命周期挂钩之前，用`@ViewChild`装饰器获取引用是不可靠的。

最重要的是，父组件不会收到子组件对属性所做的任何更改。如果子节点修改了它的`filter`属性的值，父节点的`filterTerm`属性将不会被更新。

# 4.中介服务

组件不会总是有父子关系。它们可能是不相关的，出现在应用程序的不同位置。但是如果我们需要这样的组件来通信呢？输入服务。

可以通过用`@Injectable` decorator 注释一个类来定义服务。如果我们将`providedIn`属性设置为`'root'`，该服务将被注册为单例服务。Angular 将在依赖注入链中维护服务的单个实例。

这意味着依赖于该服务的所有组件将接收同一个实例。因此，我们可以使用这样的服务将数据存储在内存中，并从相同或不同的组件中检索存储的数据。

***注意:*** *我们说的数据存储在内存中，也就是说刷新页面就不会保存数据了！*

为了在内存中存储一些数据或状态，我们通常使用带有主题的服务，更常见的是`BehaviorSubject`。

我们使用`BehaviorSubject`而不是普通的`Subject`有两个原因:

1.  不像`Subject`没有初始值，`BehaviorSubject`有初始值。
2.  如果我们在一个值发出后订阅了一个`Subject`，我们将不会收到任何东西。使用`BehaviorSubject`，我们将总是接收最后发出的值，因为它有一个初始值，我们将总是接收一个值。

我们可以从一个组件发出新的值。

在其他一些组件中，我们可以订阅接收最后发出的值。

Angular component communication demo using a service as an intermediary

***注意:*** *这看起来可能和我们之前的一个例子一样，其实不然。注意到*组件在本例*中没有父子关系。他们是兄弟姐妹。*

# 5.NgRx

如果我们的应用程序的状态是小而简单的，使用带有主题的服务就可以了。对于现实生活中的应用程序，这种情况很少发生。我们如何管理一个庞大复杂的国家？输入 NgRx。

现在，如果我们要讨论关于 NgRx 的一切，我们会以一篇很长的文章结束。这也超出了本文的范围。如果你想了解更多关于 NgRx 的信息，我们建议你查看[官方网站](https://ngrx.io/)。你也可以在媒体上阅读关于 NgRx 的内容。

下面是 NgRx 工作原理的一个非常简单的描述。

我们定义了一个`State`，它代表了将保存在`Store`中的数据格式。我们还用一些初始值定义了一个初始状态。`Store`被用作真实的单一来源。存储的状态是只读的和不可变的，这意味着它不能被直接修改。相反，当我们想要更新状态时，我们创建一个新的状态。

为了创建一个新的状态，我们需要定义并调度`Actions`。对于每组动作，我们需要定义一个`Reducer`来处理它们。reducer 是一个纯粹的函数，给定当前状态加上来自相应调度动作的数据，它会创建一个新状态。新状态再次存储在`Store`中。

最后，我们定义选择器来订阅和监听`State`中的特定变化。例如，一个组件可以订阅一个选择器来监听由另一个组件内的调度动作所引起的变化。

# 6.路线参数

如果我们只需要将一点数据从一个路由组件传递到下一个组件，那么创建一个新的服务可能不值得付出代码开销。`Router`提供了一种简单的方法。

我们如何通过路由传递数据？输入[路线参数](/angular-route-parameters-a-simple-guide-88c69d54102c)。

Angular 提供了三种类型的管线参数:必需参数、可选参数和查询参数。因为这不是一篇关于路由的文章，所以我们不打算深入细节。如果您想了解关于路由参数的更多信息，我们已经在另一篇文章中讨论了这三个参数。

[](/angular-route-parameters-a-simple-guide-88c69d54102c) [## 角度布线参数:简单指南

### 角度布线参数概述。

javascript.plainenglish.io](/angular-route-parameters-a-simple-guide-88c69d54102c) 

可以说，使用路由参数是传递小块数据的一种简单而有效的方法。此外，产生的网址是书签和共享的。

但是，请记住，指定的路由参数将出现在 URL 中。所以，不要用它们来传递用户不应该看到的复杂数据或敏感信息。

# 结论

在本文中，我们深入探讨了角度组件通信，并给出了 6 种不同的实现方式。

如果组件有父子关系，使用`@Input`和`@Output`装饰器。如果对变化的反应不感兴趣，你可以偶尔考虑一下`@ViewChild` / `@ViewChildren`装饰者。

如果组件是不相关的，使用带有一两个`BehavioSubject`的服务作为中介。相反，如果应用程序状态太大或太复杂，并且使用它证明设置它的代码开销是合理的，则使用 NgRx 进行状态管理。

最后，如果只需要将少量数据传递给下一个路由组件，请使用路由参数。

我希望你喜欢这篇文章，并且你学到了一些新的东西。如果你有，请[订阅我的时事通讯](https://vkagklis.medium.com/subscribe)获取更多类似的内容。

编码快乐！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**

****进一步阅读:****

*[](/angular-zone-js-3b5e2347b7) [## 关于 Angular 你应该知道的 10 件事

### Zone.js 是什么？如何有角度地使用它？本问答指南将回答这些问题以及更多问题。

javascript.plainenglish.io](/angular-zone-js-3b5e2347b7) [](/angular-elementref-templateref-viewcontainerref-8517b7ce3274) [## 角度 DOM 操作:ElementRef、TemplateRef 和 ViewContainerRef

### 概述 Angular 中的元素、模板、视图和视图容器，以及如何以编程方式修改 DOM。

javascript.plainenglish.io](/angular-elementref-templateref-viewcontainerref-8517b7ce3274) [](/custom-pipes-in-angular-the-ultimate-guide-e54bb400e3ce) [## 角形定制管道——终极指南

### 如何在 Angular 中创建自定义管道，什么是纯管道和不纯管道，以及如何使用纯管道来改善

javascript.plainenglish.io](/custom-pipes-in-angular-the-ultimate-guide-e54bb400e3ce)*