# 角度测试——开始编写单元测试用例的最简单方法

> 原文：<https://javascript.plainenglish.io/angular-testing-the-easiest-way-to-start-writing-unit-test-case-74b6c8df26d6?source=collection_archive---------9----------------------->

## [角度单元测试指南](https://medium.com/@kushsavani)

## 如果你是 angular 开发人员，并且从单元测试用例开始。那么这肯定会是你的初学者指南。

![](img/e573a043c948b8c0f956427261d0ad09.png)

Photo by [Blake Connally](https://unsplash.com/es/@blakeconnally?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

去年圣诞节前后，我作为一名 Angular 开发人员开始了我的旅程，我工作的一个重要部分是单元测试。我知道在开始时，我犯了很多新手的错误，并在 StackOverflow 和 GitHub 上花费了大量的时间来寻找合适的解决方案以及如何为不同的场景编写正确的测试用例。经历了几次精疲力尽之后。我发现了一种构建单元测试用例的理想方法。

# 让我们从介绍开始

自从 **Kent Beck** 开发或者重新发现 [*测试驱动开发*](https://en.wikipedia.org/wiki/Test-driven_development) *以来已经快 20 年了。这给了软件开发人员更多的责任来为他们的应用程序编写自动化测试。*

Angular 从一开始就是为了可测试而构建的。Angular 帮助您将应用程序架构定义为松散耦合组件的集合，以及基于依赖注入的 Typescript，这使得模仿依赖更加容易。有了这个好处，angular 中的单元测试就可以用 DOM 和功能来测试整个组件。在这部伟大的作品中，茉莉和业力帮助 angular 完成这个角色。

## 一些关键词和基本描述

*   `describe` :-使用“描述”功能对一系列测试进行分组。这个函数有两个参数，一个字符串和一个回调函数。
*   `beforeEach` :-这将在每个测试用例执行之前运行。在这里，它每次都会提供一个 PersonClass 的新实例。
*   `it` :-该功能用于创建特定的测试。其进入所描述的块内部。这个函数有两个参数，一个字符串和一个回调函数。
*   `expect` :-该功能确认测试正确运行并得到预测的结果。`expect`有两部分，第一部分是作为测试结果的结果值，第二部分是我们在测试结束时想要的期望值。
*   `afterEach` :- 该函数在每个测试用例运行后执行。大多数情况下，我们使用 afterEach 进行测试用例执行后的清理工作。

请记住，当您编写断言时，您应该尝试每个测试只有一个断言。当我们在一个测试中放置多个断言时，调试会变得复杂，并且每个断言必须为真，测试才能通过。

# 浅层测试 vs 隔离测试 vs 集成测试

当我们开始测试角度组件时，我们有三种可能的方法来设计测试用例:集成、浅层和隔离测试。我们不会深入探讨，但让我简化一下这项技术。

## **浅层测试**

> 浅层测试关注组件的类和模板，而不是通过模仿它们的依赖关系。

当我们谈论浅层测试时，我们主要测试组件类逻辑和模板。我们将模仿模板中的所有其他组件，或者我们可以称之为子组件。

举个例子，我们有`PersonComponent`。在组件模板中，存在一些自定义元素和指令。如果我们以正确的方式测试它，angular 将抛出告诉我们它不知道一些模板语法。另一方面，我们只想测试不包括元素的主要组件。

为了只关注组件的模板而不是它的依赖项，我们需要告诉 angular 不要试图编译那些定制元素。而这里由`schemas: [NO_ERRORS_SCHEMA]`扮演主角。这将在测试床配置中进行配置，并告诉 Angular 当它不能识别自定义元素时不要抛出任何错误。

## 孤立测试

> 独立测试只关注组件的类。

当我们为组件选择隔离测试时，我们首先主要测试组件逻辑。我们不必关注模板。即使组件包含定制元素和指令，因为隔离测试只关注组件的逻辑，模板是不相关的。

## 综合测试

> 一个集成的测试将覆盖组件及其依赖项的整体。

当我们为一个组件选择集成测试时，我们必须测试组件逻辑、它的模板以及它所有的依赖项。这意味着如果模板包含定制组件和指令，我们需要在测试床配置中注入这些依赖关系。这个测试维护起来可能更昂贵，调试起来也更困难，因为我们需要处理它所有的依赖关系。这看起来像是肤浅的测试，但我们测试更多的设计，更深入。

# 真实世界的组件测试

在一个真实的项目中，你需要测试更复杂的组件。例如，我们想测试包含菜单的`NavigationComponent`。因此，您希望只测试主要组件，而不用担心菜单。在这种情况下，我们可以使用*浅层*测试。让我们开始吧🏃…

## 导入依赖项

当我们测试一个功能完整的组件时，它需要大量的依赖项。让我们按以下顺序导入它们:

*   测试来自角度的依赖关系
*   从属关系包含在角度
*   您为此项目创建的依赖项

这些依赖项是测试模块工作所必需的。创建新组件时，Angular 已经添加了其中的一些。

**测试来自角度的依赖关系**

1.  `import { DebugElement } from '@angular/core';` —在这里，我们可以在测试过程中使用`DebugElement`来检查元件。我们可以认为它是原生的`HTMLElement`,带有一些额外的方法和属性。
2.  `import { ComponentFixture, TestBed, fakeAsync, tick } from '@angular/core/testing';`
    - `ComponentFixture` :-我们可以用它来创建一个组件的夹具，然后用它来调试。
    - `TestBed` :-我们可以使用这个类来设置和配置我们的测试。这是 Angular 为测试提供的最重要的工具之一。推荐参观 [Doc](https://angular.io/api/core/testing/TestBed) 。
    - `fakeAsync` :-使用`fakeAsync`将确保所有异步任务在执行断言之前完成。在使用`fakeAsync`的时候，我们可以用`tick`来模拟时间的流逝。它接受一个参数:向前移动时间的毫秒数，默认值为零毫秒。
3.  `import { By } from '@angular/platform-browser';` —我们可以使用`By`类来选择 DOM 元素。这个类提供了三个方法:
    - `all` :-这将返回所有的元素。没有参数需要通过
    - `css` :-使用 CSS 属性，可以选择某些元素。接受一个参数:CSS 属性。
    - `directive` :-使用指令名，选择元素。接受一个参数:指令名。
4.  `import { NoopAnimationsModule } from '@angular/platform-browser/animations';` —这个模块类将模拟动画，这允许测试快速运行，而不需要等待动画结束。
5.  `import { BrowserDynamicTestingModule } from '@angular/platform-browser-dynamic/testing';` —该模块帮助引导用于测试的浏览器。
6.  `import { RouterTestingModule } from '@angular/router/testing';` —该模块类将为测试设置路由。我们将它包括在测试中，因为一些动作将涉及改变路线。

**依赖关系包含在角度**中

这种依赖性直接来自于您在组件中使用的`@angular`。
`import { FormsModule } from '@angular/forms';` —这里的`FormsModule`是用于组件逻辑和测试的模块之一。

您为此项目创建的依赖关系

**您可以添加完成测试所需的其余依赖项。您可以添加第三方模块，如材料 UI 模块、其他组件、常量、指令、接口等。**

## **设置测试**

**因此，设置的第一步是添加`describe`块，它将作为所有测试的父，并声明我们需要的实例变量。`describe`方法创建一个包含所有测试的测试套件。**

*   **`fixture` :-这将存储一个`ComponentFixture`的实例，它包含帮助您调试和测试组件的方法**
*   **`component` :-这将存储我们组件的实例。**
*   **`rootElement` :-这将为我们的组件存储`DebugElement`，在这里我们可以访问它的子组件。**

**在这个声明之后，如果我们真正的服务进行 HTTP 调用，我们可以创建一个假的服务。这将允许我们集中精力测试组件，而不用担心处理服务。`beforeEach`的重要部分**

**现在，您声明变量和假服务，添加两个`beforeEach`块，它们将在每次测试之前执行。第一个`beforeEach`将设置`TestBed`配置。第二个将设置我们的实例变量。把它们分开是个好习惯。**

****首先** `**beforeEach**` **设置****

**`TestBed`类有一个名为`configureTestingModule`的方法。也就是配置测试模块。类似于我们在 app.module.ts 文件中使用的`NgModule`类。唯一的区别是这里的对象是一个`TestModuleMetadata`类型别名的格式。**

**这里，我们使用`overrideModule`来表示那些延迟加载组件。
让我们大致了解一下`TestModuleMetadata`可选字段。**

*   **`declarations` :-您可以在这里列出需要添加的组件**
*   **你可以在这里列出模块**
*   **`providers` :-这是用于依赖注入的**
*   **`schemas` :-添加模式以允许某些属性，如`NO_ERRORS_SCHEMA`。**

****第二个**T3**设置****

**`fixture`变量存储了来自`TestBed.createComponent`方法的类似组件的对象，您可以使用它进行调试和测试。`component`变量保存从`fixture.componentInstance`属性获得的组件。**

**`detectChanges`方法触发组件的变化检测周期。在初始化组件或更改数据绑定属性后，需要调用它。这也会渲染 DOM。**

## **添加测试**

**您已经准备好编写测试用例了。现在一切都解决了，您可以开始测试组件功能了。如果我们的组件拥有一个私有方法，我们不需要测试它，因为测试组件的公共 API 会测试它们。一般来说，你不需要测试私有方法。如果一个方法重要到需要测试，你应该考虑把它公开。**

**对于每一个测试用例来说，`detectChanges`都会起到重要的作用。在产品中，Angular 使用运行变更检测的区域，但是在单元测试中，我们没有这种机制。相反，我们需要在对组件进行更改后，在测试中频繁调用`detectChanges`。**

**关于在测试用例中写什么，这完全基于你的组件逻辑和模板。你可以在这里找到更多的。您需要在测试覆盖结果中覆盖整个组件。这里是[角度代码覆盖](https://angular.io/guide/testing-code-coverage)的指南。**

# **结论**

**如果你理解角度测试模块的核心特性，单元测试角度应用程序是很有趣的。我们已经浏览了一堆特性和例子，试图理解如何编写一个好的和合适的角度组件测试用例。我个人推荐你阅读[测试角度应用](https://www.oreilly.com/library/view/testing-angular-applications/9781617293641/)书，了解更多更深入的知识。**

*****感谢您的阅读，如果您发现这很有用，请为它鼓掌，并帮助其他人找到它。更多有趣的故事请关注我。*****

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。***

***报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*******

*******对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*****