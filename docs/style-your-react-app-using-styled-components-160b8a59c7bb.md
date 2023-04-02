# 使用样式化组件对 React 应用进行样式化

> 原文：<https://javascript.plainenglish.io/style-your-react-app-using-styled-components-160b8a59c7bb?source=collection_archive---------5----------------------->

## Styled-components 是 React & React Native 编写和管理 CSS 的库。

![](img/e7d3a14608c473cfe69b44957b33fc59.png)

Photo by [Mitchell Griest](https://unsplash.com/@griestprojects?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从 Web1.0 开始到 Web3.0，Web 技术经历了多次发展。从静态到动态的网站，jQuery 到今天的 React，Next.js，Angular，或者 vue . js——JavaScript 库和框架。如果你注意到近年来网站或 web 应用程序样式化方法的进步，我们现在有多种编写 CSS(级联样式表)的方法。我们已经看到，使用了一些功能丰富的 CSS，如 SAAS，LESS，BEM 等。我们可以从希望包含在应用程序中的 CSS 方法列表中进行选择。

如果你正在寻找模块化的 CSS 架构，就像 React 一样，并保持你的代码库整洁，[**styled-components**](https://github.com/styled-components/styled-components)将帮助你解决这个问题。

# 先决条件

在处理样式化组件之前，建议对 React 或 React-Native 开发有一个基本的了解。

# 样式组件概述

**styled-components** 是 React & React Native 编写和管理 CSS 的库。它们允许您在 JavaScript 中编写 CSS(CSS-in-JS ),使您的 CSS 与单个组件的 JavaScript 非常接近。

允许你写真正的 CSS 代码来设计你的组件。它还删除了组件和样式之间的映射。

# 开始使用样式组件

首先，我们需要将`styled-components`安装到我们的 React 项目中。

```
npm install styled-components
```

在您使用 **styled-components** 的每个组件上，您需要添加这个导入。

```
import styled from 'styled-components';
```

你可以在这里查看**样式组件**库详情[。](https://www.npmjs.com/package/styled-components/v/4.1.3)

# 创建样式化组件

安装完**样式组件**依赖项后，让我们创建第一个样式组件。我们将创建一个表单组件，它有一个接受电子邮件的`input`字段和一个提交输入的电子邮件的`button`。

对于`input`字段和`button` ***，*** 我们将分别创建名为`StyledInput`和`StyledButton`的样式化组件。

在上面的代码片段中，我们使用了内部实用方法`styled`，它将样式从 JavaScript 转换成实际的 CSS。接下来是 *HTML* *元素*我们想要 style - `styled.button`，然后添加反勾号来表示我们添加常规 CSS 语法的模板。

```
const StyledButton = styled.button`
   background-colour: blue;
   color: white;
   padding: 1rem 2rem;
`
```

类似地，对于`StyledInput`，我们使用`styled.input`继续 CSS 代码。

```
const StyledInput = styled.input`
    width: 400px;
    height: 34px;
    outline: none;
`
```

在`FromContainer`组件中返回的`<StyledButton>`和`<StyledInput>`看起来像一个普通的 React 组件。这是因为它是一个反应元件！

# 处理伪选择器和媒体查询

为响应式组件添加媒体查询很简单。只需在模板文本中编写媒体查询，如下所示。

```
...
const StyledButton = styled.button`
   background-colour: blue;
   color: white;
   padding: 1rem 2rem; @media (min-width: 768px) {
      padding: 2rem 4rem;
      width: 11rem;
   } @media (min-width: 1024px) {
      padding: 4rem 8rem;
      width: 13rem;
   }
`
...
```

类似于向样式化组件添加媒体查询，添加伪选择器非常简单。例如:

```
...
const StyledButton = styled.button`
   background-colour: blue;
   color: white;
   padding: 1rem 2rem; :hover {
     border-color: green;
   }
`
...
```

# 在样式化组件中使用 React 属性

因此，当您创建一个样式化的组件时，您实际上创建的是一个带有样式的 React 组件。在我们前面的例子中，`StyledButton`是样式化的组件，它将被呈现为一个包含样式的 HTML 按钮。

如果样式组件是 React 组件，那么我们也可以在样式组件中使用 props。因为样式化组件是功能性的，所以我们可以动态地样式化元素。

正如你在上面的代码中看到的，我们只创建了一个样式组件`Block`，并使用 ***颜色*** 道具来改变背景。这有助于使用 props 有条件地修改 CSS。

我们使用样式组件提供的回调函数来有条件地改变样式。

# 全局样式

现在，如果您想要覆盖全局样式——例如，您想要更改`body`元素的背景和字体。你可以用`createGlobalStyle`来实现这个。建议在顶层组件或一般 App.js 中使用`createGlobalStyle`，在多个页面上共享，而不是在单个页面上使用。

# 优点和结论

与传统的 CSS 方法相比，样式化的组件有很多优点。其中一些将是易于理解的语法。所有未使用的 CSS 和样式都会被自动移除，即使它们是在代码中声明的。

您不需要编写任何类名，它们是自动生成的，因此不需要管理 CSS 类命名方法。

有了 CSS-in-JS，CSS 选择器的作用域自动限定在它们的组件上。这使得知道如何编辑一个组件的 CSS 变得更加容易，因为对于如何以及在哪里使用 CSS 从来没有任何混淆。

感谢您阅读这篇文章，希望这篇文章将有助于建立您的应用程序风格！干杯！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*