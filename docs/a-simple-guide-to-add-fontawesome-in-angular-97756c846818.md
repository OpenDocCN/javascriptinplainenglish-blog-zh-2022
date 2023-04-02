# 在 Angular 中添加字体的简单指南

> 原文：<https://javascript.plainenglish.io/a-simple-guide-to-add-fontawesome-in-angular-97756c846818?source=collection_archive---------3----------------------->

## 让我们将这些令人敬畏的图标添加到我们令人敬畏的应用程序中

![](img/75e69ccb594a156477563dac3a8d293d.png)

Photo by [Daniel J. Schwarz](https://unsplash.com/@danieljschwarz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都知道网络发展的速度有多快。网络用户一天比一天聪明。现在，我们不需要写一段文字来告诉用户点击某个东西可以执行什么样的操作。

举个例子，假设我们在 web 应用程序上为用户提供了一个导出功能。那我们就不用写‘导出’通知用户了。相反，我们可以使用一个导出图标，聪明的用户会明白它会导出数据。

厉害！但现在的问题是，我们从哪里可以得到这些图标？我们必须自己建造它们吗？

放心吧！正如我所说的，web 开发发展非常迅速。我们有很多库，我们可以简单地导入到我们的应用程序中，我们可以利用这么多的图标。其中一个就是 [FontAwesome](https://fontawesome.com/) 。

在讨论实现之前，先说一下这个库是什么。

## 什么是 FontAwesome

FontAwesome 是一个免费的图标工具包，包括 1500 多个免费图标，使用起来非常简单。图标的设计考虑到了可缩放的向量，当 CSS 尺寸和颜色应用于它们时，它们会保留原来的尺寸和颜色。因此，它们是高质量的图标，在任何屏幕尺寸上都很好看。

在 Angular 5 之前，开发人员必须安装字体 Awesome 包，并在 Angular 项目中引用它的 CSS 才能使用它。

然而，Angular 5 中 FontAwesome 角度组件的创建使得将 FontAwesome 合并到我们的项目中变得很简单。字体牛逼现在可以很容易地集成到我们的项目，感谢这个功能。

现在，让我们从今天讨论的话题开始。

为了这个演示，让我们创建一个新的 angular 应用程序。

```
ng new demo-angular-fontawesome
```

现在，执行下面提到的命令来安装所需的 fontawesome 包和依赖项。我们可以使用`npm`或`yarn`来安装这些。

```
npm install @fortawesome/angular-fontawesome
npm install @fortawesome/fontawesome-svg-core
npm install @fortawesome/free-solid-svg-icons// ORyarn add @fortawesome/angular-fontawesome
yarn add @fortawesome/fontawesome-svg-core
yarn add @fortawesome/free-solid-svg-icons
```

## 在角度应用中使用字体牛逼图标

使用`angular-fontawesome`有两种方法。每一种都有自己的优点和缺点，所以由你来决定如何使用这个库。

*   显式引用
*   图标库

> 这里需要注意的一点是，无论我们使用哪种方法来集成`angular-fontawesome`，只有那些我们正在使用或导入的图标会被添加到包中。在构建期间，Angular 将忽略所有其他未使用的图标。

让我们来讨论这两种方法。

## 1.显式引用

显式引用方法需要从 npm 包中导入图标定义，将其分配给组件的属性，并将该属性绑定到`fa-icon`组件的图标输入。

虽然这种方法比图标库方法更加冗长，但是它使得确定在哪里或者是否使用给定图标变得更加容易。例如，IDE 的查找使用实例功能。这种方法的另一个优点是，如果一个图标丢失了，就会产生一个编译时错误。

用这种方法，安装`angular-fontawesome`后，打开`app.module.ts`，导入`FontAwesomeModule`，如下图所示:

```
import { FontAwesomeModule } from '@fortawesome/angular-fontawesome'
imports: [
    BrowserModule,
    AppRoutingModule,
    FontAwesomeModule
  ],
```

然后打开`app.component.ts`并导入您想要使用的图标名称。让我们假设我们希望使用`faCoffee`:

```
import { faCoffee } from '@fortawesome/free-solid-svg-icons';
```

之后，我们创建一个名为`faCoffee`的变量，并将导入的图标赋给它，这样我们就可以在`app.component.html`中使用它。我们将无法使用它，除非我们这样做:

```
faCoffee = faCoffee;
```

现在，在`app.component.html`中，编写下面的代码:

```
<div>
    <fa-icon [icon]="faCoffee"></fa-icon>
</div>
```

现在，只需运行 serve 命令`ng serve`，您将看到图标已成功导入并在我们的应用程序中使用。

## 2.图标库

尽管图标库方法使得在模板中使用更容易，但是图标必须与组件分开控制。这涉及到长期的维护问题，因为这意味着没有直接的方法来判断特定的图标是否在使用中。因此，如果无意中从图标库中删除了一个图标，程序仍将执行，但需要它的组件将在运行时失败。

函数`FaIconLibrary.addIcons()`和`FaIconLibrary.addIconPacks()`应该只在 AppModule 的构造函数中使用一次来注册图标。添加到库中的图标将出现在程序中的任何地方，并且可以简单地通过它们的名称来引用。与显式引用技术相反，这避免了手动导入图标并将其分配给每个单独组件的属性以便在模板中使用它们的需要。

要使用这种方法，在`app.module.ts`中做以下改变:

*   导入`{ FontAwesomeModule, FaIconLibrary } from '@fortawesome/angular-fontawesome'`。
*   将`FontAwesomeModule`添加到`imports`中。
    注意，由于角度模块封装，您需要将`FontAwesomeModule`添加到您想要使用`fa-icon`组件的每个模块的`imports`中。
*   将`FaIconLibrary`注入到模块的构造函数中。
*   导入一个类似`{ faCoffee } from '@fortawesome/free-solid-svg-icons'`的图标。
*   用`library.addIcons(faCoffee)`将图标添加到库中。

```
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FontAwesomeModule, FaIconLibrary } from '@fortawesome/angular-fontawesome';
import { faCoffee } from '@fortawesome/free-solid-svg-icons';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FontAwesomeModule],
  bootstrap: [AppComponent]
})
export class AppModule {
  constructor(library: FaIconLibrary) {
    // Add an icon to the library for convenient access in other components
    library.addIcons(faCoffee);
  }
}
```

现在只需将这些变化添加到`app.component.html`

```
<!-- simple name only that assumes the default prefix -->
<fa-icon icon="coffee"></fa-icon>
<!-- ['fas', 'coffee'] is an array that indicates the [prefix, iconName] -->
<fa-icon [icon]="['fas', 'coffee']"></fa-icon>
```

> 也可以使用`constructor`中的`library.addIconPacks(fas, far);`导入整个图标样式。但是要谨慎！因为这种导入图标的方法不支持树摇动，所以来自导入包的所有图标都将在包中结束。

## 哪种方法更好？

我们已经看到了在 Angular 应用程序中集成字体 Awesome 的两种方法。现在的问题是用哪一个。

显然，这两种方法都有自己的好处。你要用哪一个完全取决于你自己。但是如果这个很难决定，我们可以考虑建筑尺寸。

为了测试它，我在我们的演示应用程序中创建了 5 个测试组件，并为每个组件添加了一个图标。然后我简单地使用`ng build — prod`构建应用程序。

带有**显式引用**的构建大小为`276.37 kB`，带有**图标库**的构建大小为`276.33 kB`。

正如我们所看到的，在构建大小上有一个小的差异。虽然差别不是很大，但这仅适用于演示应用程序。对于大型应用程序来说，它肯定会产生巨大的影响。

因此，如果你在这两种方法之间挣扎，你可以考虑你的应用程序的构建规模来决定。

## 图标风格的字体真棒

我们将查看免费图标，不包括 Pro light 图标，这些图标带有前缀`fal`和专业许可证。

*   实心图标使用前缀`'fas'`并从`@fortawesome/free-regular-svg-icons`导入
*   常规图标使用前缀`'far'`并从`@fortawesome/free-solid-svg-icons`导入
*   品牌图标使用前缀`'fab'`并从`@fortawesome/free-brands-svg-icons`导入

## 改变图标的颜色和大小，而不用编写 CSS 样式

让我们看看如何在 Angular 中修改字体图标的颜色，而不必编写 CSS 样式。

这个方法使得在组件级别使用图标成为可能。然而，当在所有组件中使用这种策略时，它是无效的，因为图标颜色会在我们项目的组件中的任何地方改变。我们可以使用 CSS 类或样式属性为多个组件修改一次。

但是，我们可以在处理组件级别时使用它，因为我们将只在该组件中使用图标，而不是为它添加 CSS 属性并在 CSS 文件中对其进行样式化。那么，让我们看看如何在一个角度项目中完成这个。下面的图标默认为黑色，我们想将其改为红色:

```
// from black
<fa-icon [icon]="['fas', 'coffee']"></fa-icon>

// to red
<fa-icon
      [icon]="['fas', 'coffee']"
      [styles]="{ stroke: 'red', color: 'red' }"
></fa-icon>
```

使用内嵌样式改变图标颜色和笔画时，必须使用`fa-icon`属性。

接下来，我们将使用 Angular 的内嵌样式将图标的大小从小变大。为此，我们需要使用`fa-size`图标的属性:

```
<fa-icon [icon]="['fas', 'coffee']" [styles]="{ stroke: 'red', color: 'red' }" size="xs"></fa-icon><fa-icon [icon]="['fas', 'coffee']" [styles]="{ stroke: 'red', color: 'red' }" size="sm"></fa-icon><fa-icon [icon]="['fas', 'coffee']" [styles]="{ stroke: 'red', color: 'red' }" size="lg"></fa-icon><fa-icon [icon]="['fas', 'coffee']" [styles]="{ stroke: 'red', color: 'red' }" size="5x"></fa-icon><fa-icon [icon]="['fas', 'coffee']" [styles]="{ stroke: 'red', color: 'red' }" size="10x"></fa-icon>
```

默认情况下，字体超棒图标继承父容器的大小。它允许它们匹配我们使用的任何文本，但是如果我们不喜欢默认的大小，我们必须给它们我们想要的大小。

使用等级 xs、sm、lg、5x 和 10x。这些类根据我们的喜好改变图标的大小。

## 动画字体真棒图标

让我们看看如何在不使用 CSS 或动画库的情况下，在 Angular 中动画显示字体牛逼的图标。

作为一名开发人员，我们可能希望在用户单击提交按钮或页面正在加载时显示加载器或旋转器效果，以通知用户正在加载某些内容。

为此，我们可以使用字体很棒的图标。我们可以将字体 Awesome spin 属性应用于图标标签，而不是导入一个额外的 CSS 动画库。

这使我们不必为了使用微调效果或使用关键帧编写大型 CSS 动画而下载整个 CSS 动画库。

```
<fa-icon [icon]="['fas', 'spinner']" [styles]="{ stroke: 'red', color: 'red' }" size="10x" [spin]="true"></fa-icon>
```

当我们加载页面时，微调图标将无限期地旋转。这是因为`spin`属性已经被设置为`true`。

> 就像我们调整图标的大小、制作图标的动画和样式一样，我们可以对这些图标做更多的事情，这一点我们可以从[官方文档](https://github.com/FortAwesome/angular-fontawesome/blob/HEAD/docs/usage/features.md)中了解到。

```
**Want to Connect?**Connect with me on [LinkedIn](https://www.linkedin.com/in/gouravkajal/).
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*