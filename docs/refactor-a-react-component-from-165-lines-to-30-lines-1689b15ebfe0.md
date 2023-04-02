# 将 React 组件从 165 行重构为 30 行

> 原文：<https://javascript.plainenglish.io/refactor-a-react-component-from-165-lines-to-30-lines-1689b15ebfe0?source=collection_archive---------3----------------------->

## 使用 React 挂钩形式和材质 UI 清理 React 组件

![](img/a4b70c90463a004090fec8869a0d7e4b.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

React Hook Form 是 React 生态系统中最流行的处理表单输入的库之一。

但是，如果您使用任何类型的组件库，让它正确集成可能有点棘手。

今天，我将向您展示如何使用 React Hook 表单集成 Material UI 的各种组件。

让我们开始吧。

# 先决条件

关于如何使用`react-hook-form`，我就不多赘述了。如果你还不知道如何使用`react-hook-form`，我强烈建议你先看看这篇文章

[](/how-to-use-react-hook-form-with-typescript-2cf597c0c45f) [## 如何在 TypeScript 中使用 React Hook 表单

### 为您的应用程序构建高性能、简洁的表单

javascript.plainenglish.io](/how-to-use-react-hook-form-with-typescript-2cf597c0c45f) 

我只能说，你不会后悔学习这个图书馆。

# 起始代码

让我们看看我们将要开始的代码。

FormBadDemo.tsx

这是一个非常标准的表格。我们使用了一些最常见的表单输入。但是这个组件有些问题。

*   `onChange`经手人重复。如果我们有多个文本输入，我们需要管理这些个人，这是非常令人沮丧的。
*   如果我们想要处理错误，那么它们的大小和复杂性将会爆炸。

# 主要思想

如你所知，`react-hook-form`与 HTML 的默认输入组件配合得非常好。但如果我们使用各种组件库，如 Material-UI 或 Ant design 或任何其他组件库，情况就不一样了。

为了处理这些情况，`react-hook-form`所做的是导出一个名为`**Contrtoller**` **的特殊包装组件。如果你知道这个特殊的组件是如何工作的，那么将它与任何其他库集成将是小菜一碟。**

控制器组件的框架如下所示。

如果您已经完成了基本的表单处理(我确信您已经完成了)，那么您应该知道两个字段对于任何输入组件都是重要的。一个是`value`，另一个是`onChange`。

因此，我们的`Controller`组件将这两个属性以及`react-hook-form`的所有其他魔力注入到组件中。

其他一切都像魔咒一样管用！让我们看看它的实际效果。

# 表单输入道具

每个表单输入都需要两个基本属性。分别是`name`和`value`。这两个属性控制所有功能的功能。

所以，为此添加一个类型。如果你使用 javascript，你不需要这个。

FormInputProps.ts

# 文本输入

这是我们首先需要处理的最基本的组件。下面是一个用 material UI 构建的独立文本输入组件。

FormInputText.tsx

在这个组件中，我们使用了`control`属性表单`react-hook-form`。我们已经知道这是从`useForm()`库的钩子上导出的。

我们还展示了如何显示错误。对于其余的组件，为了简洁起见，我们将跳过这一步。

# 无线电信号输入

我们第二常见的输入组件是`Radio`。与`material-ui`整合的代码如下。

我们需要一个`options`数组，在其中我们需要传递该组件的可用选项。

如果你仔细观察，你会发现这两个组件在用法上非常相似。

# 下拉输入

我们的下一个组件是下拉菜单。几乎任何形式都需要某种下拉菜单。组件的代码如下所示

FormInputDropdown.tsx

在此组件中，我们已经删除了显示标签的错误。它就像无线电组件一样

# 日期输入

这是一个普通而特殊的组件。在材质界面中，我们没有任何开箱即用的`Date`组件。我们需要一些助手库。

首先，安装那些依赖项

```
yarn add @date-io/date-fns@1.3.13 @material-ui/pickers@3.3.10 date-fns@2.22.1
```

小心版本。否则，可能会出现一些奇怪的问题。我们还需要用特殊的包装器包装我们的数据输入组件。

FormInputDate.tsx

我选了`date-fns`。可以像`moment`一样挑别人。

# 复选框输入

这是最棘手的部分。没有明确的例子说明如何使用这个组件和`react-hook-form`。为了处理输入，我们必须做一些手工劳动。

我们在这里控制选定的状态，以正确处理输入。

FormInputCheckbox.tsx

现在你只需给它一个选项列表，一切都会变得非常好！

# 滑块输入

我们的最后一个组件是一个`Slider`组件。这是一个相当常见的组件。代码很容易理解

您可以自定义`handleChange`函数，使其成为两端滑块组件(对时间范围有用)。将`number`改为`number[]`即可

# 把所有东西都钩在一起

现在让我们在最终表单中使用所有这些组件。这将利用我们刚刚制作的可重复使用的组件。

FormDemo.tsx

最后，我们的表单看起来像这样。是不是很棒？

我希望你今天学到了一些东西。祝您愉快！

**有话要说？通过**[**LinkedIn**](https://www.linkedin.com/in/56faisal/)联系我

## 资源:

*   **视频格式:**【https://www.youtube.com/watch?v=aaj6YCil1p4 
*   **Github Repo:**[https://Github . com/Mohammad-fais al/react-hook-form-material-ui](https://github.com/Mohammad-Faisal/react-hook-form-material-ui)

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***

[](/story-of-a-failed-react-project-f32177479bdf) [## React 项目失败的故事

### 这给我们的创业带来了灾难。

javascript.plainenglish.io](/story-of-a-failed-react-project-f32177479bdf) [](/45-npm-packages-to-solve-16-react-problems-a9ab18946224) [## 45 个 NPM 软件包解决 16 个 React 问题

### 关于如何选择完美的 npm 包的深入指导

javascript.plainenglish.io](/45-npm-packages-to-solve-16-react-problems-a9ab18946224)