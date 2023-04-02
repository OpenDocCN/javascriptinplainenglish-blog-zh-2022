# Angular 中组件通信的基础

> 原文：<https://javascript.plainenglish.io/basics-of-component-communication-in-angular-82fc196f30f9?source=collection_archive---------5----------------------->

## 理解组件交互对于理解角度是必不可少的。下面是让组件进行通信的基本方法。

![](img/f69f09bf254d30ff2051b4e97cadbbaf.png)

Photo by [Pavan Trikutam](https://unsplash.com/@ptrikutam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

像其他前端框架一样，组件是 Angular 的基石。所以，知道如何让组件互相通信，对 Angular 开发至关重要。让我们看看组件与一个或多个其他组件通信的几种方式。

## 1.调用子组件中的函数

父子关系是组件交互的最常见需求。假设我们有一个`ProfileComponent`，其中有一个`ProfilePictureComponent`。当用户点击`ProfileComponent`中的按钮时，我们想调用一个函数来改变`ProfilePictureComponent`中的图像。我们可以通过在父组件中使用`ViewChild`装饰器来实现这一点:

`ViewChild`装饰器可以用来引用作为子元素存在的`@Component`或`@Directive`。它接受一个选择器，在我们的例子中是子组件`ProfilePictureComponent`。现在我们可以简单地引用组件并公开调用它的任何可用方法。例如:

## 2.将数据传递给子组件

如果我们不想调用子对象中的方法，而是想传递一个值给子对象，会怎么样？在这种情况下，我们可以利用子组件中的`Input`装饰器。看看我们的子组件:

`Input` decorator 充当实例化组件的模板和组件本身的属性之间的绑定。在变化检测期间，Angular 会将模板值传递给组件值，确保它们被绑定。换句话说，在我们的父模板中，我们可以实例化 ProfilePictureComponent:

```
<profile-picture [pictureURL]="currentImageURL"></profile-picture>
```

通过将`currentImageURL`传递给子节点，我们可以将它们绑定在一起，允许我们更改父节点中的值，并查看子节点中反映的更改。

## 3.调用父组件中的函数

在示例 1 中，我们调用了子组件中的一个函数。如果我们想反过来调用父类中的函数呢？这就是我们可以利用`Output`装饰器的地方。在我们的子组件中:

使用`Input`装饰器，数据从父模板流向子组件；使用`Output`装饰器，数据从子组件流向父模板。现在，在我们的父模板中，我们可以有:

```
<profile-picture (changeImage)="reloadImage($event)"></profile-picture>
```

注意，`changeImage`被圆括号而不是方括号包围，这意味着我们绑定到一个输出，而不是一个输入。我们将父节点的`reloadImage`方法传递给这个输出，现在每当子节点发出一个事件时`reloadImage`就会被调用。

要发出一个事件，我们必须调用我们的`EventEmitter`上的`emit()`方法，并传递预期的数据类型，我们已经将其指定为`string`:

通过变化检测的能力，Angular 将把`img`值向上传递给父节点。

## 4.父子之间的双向数据

`Output`装饰器不仅可以用来调用父组件中的方法，还可以用来传递值。这是显而易见的，在我们之前的例子中——`img`值被直接传递给父节点。但是我们可以将它与一个`Input`结合起来，以实现双向数据流:子节点中的更改将传播到父节点，而父节点中的更改将向下传递到子节点。让我们把`ProfilePictureComponent`改成这样:

为了让这种双向流与 Angular 的盒中香蕉语法一起工作，`Output` **必须**遵循精确的命名约定。`Output`变量名必须是`Input`的名称加上单词“Change”因此，如果你有一个名为“颜色”的`Input`，那么`Output`将被命名为“颜色变化”遵循这个约定，我们可以在父模板中使用香蕉盒语法来实现双向绑定:

```
<profile-picture [(img)]="image"></profile-picture>
```

通过这个方法，我们可以改变父节点的`image`变量，并让它流向子节点，子节点可以使用它的本地`changeImage()`方法将改变发送给父节点。

## 5.向不相关的组件“广播”数据

到目前为止，我们所有的例子都包括父子关系中的两个组件。但是有时一个组件需要将数据发送给页面中某个不相关的组件。实现这一目标的最佳方式之一是将订阅与角度服务相结合。

让我们修改我们的例子。现在，它需要与页面上其他地方的`ContactCardComponent`通信，而不是父`ProfileComponent`与子通信。我们不能使用直接的属性绑定，因为这两个组件是互不可知的。相反，我们可以创建一个服务来存储和处理数据中的变化，并将这些变化传递给任何选择订阅的组件。

这里我们有一个私有的`contactInfoSubject`，它将是负责联系方式变更的主体。public `contactInfoStream`是任何组件都可以订阅的可观察对象，以便从`contactInfoSubject`接收更新。类似地，任何组件都可以调用`changeContactInfo()`方法来触发主题的变化。由于 Angular 的依赖注入，服务的同一个实例将在我们注入的任何组件中使用，允许数据同步。

我们可以创建一个`ContactCardComponent`,如下所示:

在`ngOnInit`生命周期挂钩中，我们订阅了在`ContactService`中创建的主题，这样无论何时主题发送一个新值，本地`contactInfo`字符串都会被更新以匹配。组件也有自己的方法来调用`changeContactInfo()`方法，这样它也可以触发自己的更改。

使用这些方法，我们可以在服务中订阅主题的任意数量的组件之间同步数据，而不必依赖父子关系。

我希望您发现组件通信的基础知识是有用的。下面您将找到有助于加深理解的资源。一如既往的感谢您的阅读。

 [## 有角的

### Angular 是一个构建移动和桌面 web 应用程序的平台。加入数百万开发者的社区…

angular.io](https://angular.io/guide/inputs-outputs)  [## 有角的

### Angular 是一个构建移动和桌面 web 应用程序的平台。加入数百万开发者的社区…

angular.io](https://angular.io/guide/two-way-binding)  [## RxJS

### 编辑描述

rxjs.dev](https://rxjs.dev/guide/subject) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*