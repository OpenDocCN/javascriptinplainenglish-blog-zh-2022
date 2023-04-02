# 阿斯特罗:评估街区的新成员

> 原文：<https://javascript.plainenglish.io/astro-evaluating-the-new-kid-on-the-block-c3fec119df1?source=collection_archive---------14----------------------->

![](img/2cff7b211c296c8eb70e12c4ac8676f0.png)

近年来，大规模[微前端应用(MFEs)](https://www.itmagination.com/blog/what-are-micro-frontend-web-applications-mfes) 和[高性能多页面应用(MPAs)](https://www.itmagination.com/clients-scope/web-application-development) 的使用和需求不断增加。尽管许多技术爱好者对此类应用程序的一些概念还很陌生，但今天，有大量的工具可以高效、广泛地开发可伸缩的、更高效的前端应用程序。

我们将关注 Astro，这是一个多页面应用程序(MPA)开发框架，它引入了新的令人兴奋的方法，使用一个称为“Astro Islands”的概念来更好地处理前端应用程序中的多个前端模块和独立组件。

在本文中，我们将详细介绍使用 Astro 构建大规模多框架前端项目或者简单地将现有套件、门户或 web 应用程序迁移到运行在 Astro 上的 MFE 架构的一些挑战和可能性。目的是提出新的静态站点生成器作为大、中、小型项目的潜在选择，同时概述潜在的问题和挑战。由于我们将使用 Astro 集成多个框架，我们将尽量不要深入复杂的细节，以保持阅读简短，同时仍然让您的时间物有所值。

# Astro 很少做与同行不同的事情

Astro 中有一些特性和功能值得一提，因为大多数人可能习惯于使用其他技术和架构构建大型应用程序，这里有一些 Astro 与其他框架和库不同的地方。

# 组织、编译和呈现组件的多页方法(MPA)

虽然多页面应用程序(MPAs)并不是一个新概念，但今天的许多 web 应用程序都是单页面应用程序(spa)，尤其是基于 React、Angular 或 Vue 的应用程序。复杂的 MFE 组件和项目从 MPA 架构中受益匪浅，因为它降低了复杂性，并在渲染、优化、安全、路由和应用程序的其他方面提高了应用程序的整体性能，因为默认情况下 Astro 带有服务器端渲染(SSR)并在幕后处理大量进程。这反过来又减少了浏览器做出基本决策的时间。然而，值得注意的是，并非所有的应用程序都受益于 MPA 架构，在投入时间之前，应该理解两者的区别。

## 阿斯特罗群岛

Astro 引入了一个概念，叫做“Astro 岛”。该特性和其他功能允许框架将来自不同框架的组件合并到一个页面中，而不会出现一个框架或库影响另一个框架或库的冲突或问题。

## 基于默认文件结构的路由支持

创建项目后，无需任何额外设置的内置默认路由设置。没有额外的配置文件或任何设置来启动和运行基本路由。无需专门定义路由或配置路径；一切都基于您拥有的页面以及它们在各自文件夹中的命名/放置方式。如果需要配置更复杂的路由情况，Astro 确实为开发人员提供了一种轻松定制路由的方法。总的来说，仅仅通过使用这个特性就可以加速建立 Astro 项目的过程。

## 大量集成

Astro 为开发人员提供了一系列官方插件，这些插件支持与第三方库、工具、框架和无服务器解决方案的集成。添加对 React、Vue 和 Netlify 等工具的支持就像使用 Astro 命令行工具运行命令一样简单。

## Astro 命令行界面(CLI)

虽然命令行工具不是最创新的东西，但值得一提的是 Astro CLI 不仅仅是构建和创建新项目。它还为开发人员提供了一些命令，如添加对第三方工具的支持、服务于项目、类型检查和其他用于日常开发的有用命令。

# Astro 如何让开发复杂应用程序的过程变得更简单？

*   Astro 自带命令行工具 Astro CLI，与 Angular 类似
*   Astro 为他们的项目提供了优秀的、有组织的文档，你可以在这里找到[https://docs.astro.build/en/getting-started/](https://docs.astro.build/en/getting-started/)
*   Astro 提供了多种方式来管理项目中的样式，并额外考虑了动态样式、范围以及管理和填充项目中样式变量的有趣方式。
*   使用文件结构/目录的自动路由确保您做最少的工作来使您的项目路由到位，尽管 Astro 提供了定制路由和行为的机会，但许多项目可能不需要在这方面做任何事情。
*   出色的数据绑定，通过 Astro 指令、参数和数据注入生成静态和动态内容，在不同的应用领域提供，并完成数组和其他复杂对象的自动渲染。
*   一个易于使用的 API 通信接口，通过内置的获取支持来请求内容和数据

# 使用 Astro 有哪些缺点？

*   *。astro* 文件是灵活的、可定制的和可扩展的，以支持多种框架、变量、CSS 变量的加载和许多其他事情。当谈到利用阿童木的超能力，你想用。阿斯特罗尽可能多地归档那些*可能需要一点时间来适应的东西。*
*   VS 代码完全支持编辑。astro 文件；WebStorm 和其他一些编辑器还不支持。在撰写本文时(2022 年 11 月 4 日)。
*   Astro 可能还没有正式支持你喜欢的框架、工具或库。需要使用第三方解决方案集成的角形组件就是一个例子

对于那些已经熟悉 MPA 的人来说，如果你理解在 MPA 中利用 cookies、本地和会话存储、缓存、查询/路径变量以及通常只存储你需要的基本内容来处理数据的概念，你会同意我的观点，这一点并不是一个很大的缺点。从架构的角度来看，这也是一件好事，因为它鼓励你的独立组件“真正独立”。

# 建立一个天文项目

建立一个 Astro 项目很容易，部分原因是命令行工具可用。其中一个可用的命令是创建命令，它提供了创建一个新项目的可能性 *npm create astro@latest* 一旦该命令被执行，一个新的项目就会生成，它为您提供了一个开始工作的模板。如果您不需要 starter 模板，可以很容易地选择空白项目选项，默认情况下，支持。天文文件，。html 文件和自定义 web 组件从一开始就包含在基本的 Astro 项目中。

# 构建大型多框架项目

使用 Astro，可以将多个框架合并到一个项目中。这个想法对许多人来说可能会觉得奇怪。这种实现有很多用例，**尤其是**包含各种独立功能的产品，或者多个团队开发需要在同一个包装器项目中一起工作的独特功能的产品。在大多数情况下，公司可能使用相似的技术，在其他情况下，在特性的第一次迭代和当前迭代中使用的技术可能有很大的差异。在大多数情况下，当涉及到一个大型产品时，Astro 隔离组件的“孤岛”方法有助于正确分离许多独立组件。这个功能是如此强大，以至于我可以说它使得在一个 Astro wrapper 项目中使用不同的框架/技术成为可能。

*   Astro 自己的组件
*   纯 Html，CSS，JS 文件
*   本机 Web 组件
*   发光元件组件
*   反应组分
*   Vue 组件
*   角度分量

对于我们的示例，我们将考虑将使用以下技术的项目捆绑到我们的示例 Astro wrapper 项目中:

对于 Astro 组件，我们使用 starter 模板附带的默认组件，并添加了一些简单的 html 页面和 JS。Astro 在渲染自己的组件或处理常规 html、css 和 js 文件时没有任何问题。代码样本可以在[https://github . com/itmaginationdemos/astro-multi framework-demo](https://github.com/itmaginationdemos/astro-multiframework-demo)上看到。

## 本机 Web 组件支持

使用 *create-astro* 命令行工具，一个新项目很快就生成了。由于 Astro 使用文件结构提供了内置的路由，因此在 pages 子文件夹下创建了一个新文件夹。

我们不需要安装任何额外的插件来使用 astro 中的自定义 web 组件，因为它是默认支持的。创建新项目后，我们可以继续创建一个定制的 web 组件及其 html、css 和 js 代码，并将其添加到。页面/web 组件子文件夹下的 astro 文件。

```
--- 
import Card from '../../components/Card.astro';
import { CustomWebComponent } from '../../components/custom-web-component.js';
--- 
<script src="./src/components/custom-web-component.js" type="module"></script>
<main> 
  <Card 
    href="/" 
    title="Back to home page" 
    body="navigates back to /pages and loads the default index file"
  />
  <custom-web-component count="2"></custom-web-component> 
</main>
```

该项目编译成功，我们可以看到组件呈现的功能工作。

**注:** *同。只要 astro.config.mjs 中没有添加其他框架支持，astro 文件、Web 组件就可以正确导入和渲染。如果为任何框架添加了额外的支持，例如 React 或 Vue，自定义组件就会受到影响，astro 会尝试预渲染它，导致它遇到与 DOM 相关的问题，特别是在使用 windows 类的方法时。在这种情况下，使用 registered 标记而不是 imported 类应该可以永久地解决这个问题。*

**结论**
开箱即用的路由工作得非常好，通过属性将数据传递给组件的工作如预期一样。使用内置组件方法也可以。通过注册的标记名以及 Astro 导入的类来呈现定制组件很容易。

# Lit 元素支持

使用 astro add lit 命令，可以将 lit 元素支持自动添加到项目中。还有一个添加 lit 支持的手册指南，其中包括 astro.config.mjs 文件中要添加的包和要更改的配置。Lit 元素组件和 Astro 组件可以在同一个。astro 文件以及单独的 html 文件。

```
--- 
import Card from '../../components/Card.astro'; 
import GenericStyle from '../../styles/GenericStyle.astro'; 
import {CustomLitComponent} from '../../components/custom-lit-component'; 
--- 
<main> 
  <Card 
    href="/" 
    title="Back to home page" 
    body="navigates back to /pages and loads the default index file" 
  /> 
  <CustomLitComponent count="1"/> 
  <CustomLitComponent count="2"/> 
  <custom-lit-component count="3"></custom-lit-component> 
</main>
```

**注意:** *对于 Lit 元素，注释和带注释的属性不能开箱即用，需要额外的努力使它们可压缩。相反，我们的例子中使用了静态属性。*

**判决**

关键特性看起来是开箱即用的，但是，在将组件包含到 Astro 项目中时，有一些陷阱需要注意，其中大多数都记录在 Astro 网站上的指南中。我们发现不支持添加现成的注释，需要做一些额外的工作才能让它们工作。

# 反应组件支持

Astro 支持[反作用](https://www.itmagination.com/blog/react-18-what-changes-does-it-bring)组件。使用 MFA 框架和您现有的 [react](https://www.itmagination.com/career-paths/react) 组件非常简单，因为我们可以使用 astro add react 添加对 React 的支持，它设置了使用 React 组件所需的一切。

```
--- 
import Card from '../../components/Card.astro';
import GenericStyle from '../../styles/GenericStyle.astro';
import { CustomReactTodoApp } from '../../components/custom-react-component';
--- 
<main> 
  <Card 
    href="/" 
    title="Back to home page" 
    body="navigates back to /pages and loads the default index file"
  /> 
  <CustomReactTodoApp count="1" client:idle="react"></CustomReactTodoApp> 
  <CustomReactTodoApp count="2"></CustomReactTodoApp> 
  <CustomReactTodoApp client:only="react"></CustomReactTodoApp> 
</main>
```

**注意:** *您可能需要禁用使用客户端的服务器端呈现:仅在特定情况下='react ',其中组件需要以服务器端呈现不支持的动态方式传递 props 或呈现对内部组件的更新。这些情况可能很少见，甚至不会持续太久，因为 Astro 开发人员正在积极改进平台。*

**判决**

似乎开发人员对 React 集成非常关注，因为 React 组件可以与 Astro 无缝协作，并且目前存在的错误/集成挑战最少。对于 react 样本设置过程的大部分，react 功能都很容易实现，如上面的 Todo 列表示例所示。

# Vue 组件支持

正如 Lit 或 React 的情况一样，添加 [Vue](https://www.itmagination.com/career-paths/vue) 是一个无摩擦的过程。你所需要做的就是执行 astro add vue 命令，对 vue 组件的支持将被添加。在中使用 Vue 组件。天文文件和独立的。基于下面的例子，Astro 项目中的 html 文件是成功的。

```
--- 
import Card from '../../components/Card.astro'; 
import GenericStyle from '../../styles/GenericStyle.astro'; 
import CustomVueComponent from '../../components/CustomVueComponent.vue' 
--- 
<main> 
  <Card 
    href="/" 
    title="Back to home page" 
    body="navigates back to /pages and loads the default index file"
  /> 
  <CustomVueComponent count="1" client:visible> </CustomVueComponent> 
</main>
```

**判决**

支持 Vue 组件、特性和方法，并且集成 Vue 和 Astro 没有什么大问题。

# 角形部件支架

astro 没有官方插件来桥接 Astro 的 [Angular](https://www.itmagination.com/career-paths/angular) 组件，但 Astro 官方网站上列出了一个名为 analogjs 的第三方插件。这个插件允许我们将角度组件集成到我们的 astro 项目中，使用内置命令*Astro add @ analogjs/Astro-Angular*我们可以将对角度组件的支持添加到我们的 Astro wrapper 项目中。

乍一看，似乎 angular 包在安装时添加了最多数量的依赖项，这可能部分是因为 angular 模块/组件不是以原始/未编译的形式设计为可拆卸并添加到第三方项目中的，因此需要组成完整功能 angular 项目的所有附加依赖项，这也可能与通过第三方框架/库(analogjs)提供支持的事实有关，并且由于库的构建方式，它需要所有附加包。由于在本文中我们不涉及更小的细节，我们将把想法留给评论。

在 Astro 中创建和使用 Angular 组件需要添加一个 TypeScript 配置文件 *tsconfig.app.json* ，组件代码也要用*编写。ts* 文件，因为这是此类项目的默认设置。在这里添加 TS 支持还表明 Astro wrapper 项目中的其他组件也可以用 TypeScript 编写，如果它们的配置正确的话。

初始设置后，角度组件的变化检测不起作用,“astro run dev”命令停止工作。经过进一步调查，我们发现:

1.与没有 Angular 的 Astro 相比，Angular + Astro 项目似乎更慢，这是你设法让它工作的时候，正如 Brandon Roberts【https://github.com/brandonroberts/angular-astro-islands】T4 的例子所示

2.Astro run dev 命令在尝试访问网站时出现错误，例如内存不足，这发生在使用多个框架但在一个项目中仅使用 Angular 和 Astro 无法重现的情况下。

```
--- 
import Card from '../../components/Card.astro';
import GenericStyle from '../../styles/GenericStyle.astro';
--- 
<script src="/angular_assets/runtime.f12b6390b6dfe9bc.js" type="module"></script>
<script src="/angular_assets/polyfills.cd4b02e8647d32c8.js" type="module"></script>
<script src="/angular_assets/main.28c576b20400a3a6.js" type="module"></script> 

<main> 
  <Card 
    href="/" 
    title="Back to home page" 
    body="navigates back to /pages and loads the default index file"
  /> 
  <app-root count="1"></app-root> 
</main>
```

**注意:** *如 brandon roberts 的文章所述，角度积分支持渲染独立组件。对于在 angular framework 中独立组件支持的开发和发布之前构建的所有 Angular 项目，在项目可以与 Astro 紧密结合之前还有工作要做。*

**判决结果**

角度分量。astro 文件有点功能性。除了明显的挑战之外，在 astro 中使用 angular 确实是可能的，但是如果你的 astro 项目还将托管来自其他库的组件，那么在当前的设置中不推荐使用 angular。目前，在多框架天文项目中，Angular 框架是最大的挑战。可能有一些方法可以解决这个问题，比如构建最终的 Angular 项目，并将其作为编译后的 html、js 和 css 文件添加到 Astro 项目中，这些文件在我们的示例中可以正常工作，但是试图直接使用组件，**尤其是**当使用一个利用多个框架的健壮项目时，会带来一些挑战和困难。

值得注意的是，Angular 并不是在集成过程中面临挑战的唯一框架，正如在以前的框架中看到的那样，迁移和添加功能的过程中总会有一些缺点，但迄今为止，Astro 中对大型应用程序的 TypeScript 框架的支持是最没有希望的。

此外，通过使用新的静态站点生成器，我们解决了 JAMStack 上的角度问题。Scully 已经解决了这个问题，尽管 Astro.js 给了我们更多的灵活性。

## 在一页上使用所有组件

在实现了各种框架之后，将它们组合起来用于 Astro 项目中的任何地方是最容易的部分。组件被导入到。astro 文件和该文件的 html 部分中引用的自定义元素标记。构建或渲染这个没有问题。astro 文件，使以这种方式使用 Astro 的裁决是积极的。

```
--- 
import Card from '../../components/Card.astro'; 
import GenericStyle from '../../styles/GenericStyle.astro'; 
import {CustomLitComponent} from '../../components/custom-lit-component'; 
import AngularComponentWrapper from '../../components/AngularComponentWrapper.astro';
import { CustomReactTodoApp } from '../../components/custom-react-component'; 
import CustomVueComponent from '../../components/CustomVueComponent.vue' 
--- 
<script src="./src/components/custom-web-component.js" type="module"></script> 
<main> 
  <h1>All components in one project</h1> 
  <div class="component-block"> 
    <Card 
      href="https://docs.astro.build/" 
      title="Astro Component" 
      body="Learn how Astro works and explore the official API docs."
    /> 
    <AngularComponentWrapper count="1"/> 
    <CustomVueComponent count="1" client:visible/> 
    <CustomReactTodoApp count="1" client:idle="react"/> 
    <CustomLitComponent count="1"/> 
    <custom-web-component></custom-web-component> 
  </div> 
</main>
```

# 结论

Astro 像冠军一样处理了大部分集成工作，展示了迄今为止制作平台的出色工程技术。坦率地说，我们对结果印象深刻。

在中使用组件有一些不同。astro 文件并在。html 文件。其中一个区别是将组件从 JS 或自己的框架文件导入到。html 文件，这对每个项目都是一个挑战，因为它们要么需要作为 Astro 支持的模块加载，要么保存在公共文件夹中，以便能够通过引用源代码(例如使用 script 标签)正确导入它们。

这可能会对项目组织造成限制，尽管它可能是可定制的，但是大多数组件在它们自己的 html 文件中呈现的示例现在都以单个组件为特色，所有需要的代码都捆绑在。html 文件。我们会说这种限制是设计出来的，因为岛的概念反映在这种行为中，并迫使开发人员通过相关代码的组织和逻辑的正确封装来确保组件尽可能独立。

一般来说，我们建议使用。astro 文件，以减少正确配置这些项目以符合 Astro 所需的工作量。非常坦率地说，您可以放弃所有其他 JS 库和框架，只使用 Astro 的原生文件，尽管有时情况并非如此。

Astro 在示例项目的整个开发过程中展示了很好的前景，希望它得到更多的采用和开发时间。为这个项目制作的代码样本可以在 https://github . com/itmaginationdemos/astro-multi framework-demo 找到。反馈是最受欢迎的，你可以通过 Twitter[@ zino addi](https://twitter.com/zinoadidi)联系到本文和演示的作者。

‍

*最初发表于*[*【https://www.itmagination.com】*](https://www.itmagination.com/blog/astro-micro-frontends)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，*** *和 [***不和***](https://discord.gg/GtDtUAvyhW)*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。***