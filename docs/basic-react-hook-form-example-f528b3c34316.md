# 基本 React 挂钩形式示例

> 原文：<https://javascript.plainenglish.io/basic-react-hook-form-example-f528b3c34316?source=collection_archive---------10----------------------->

## 您是否曾经在 React 中构建表单，并发现必须构建自己的逻辑来处理错误、提交和验证检查是一件很烦人的事情？

![](img/99d3f910c2d1a10df60f9cdf76d95c9f.png)

Photo by [Scott Graham](https://unsplash.com/@homajob?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

您是否曾经在 React 中构建表单，并且发现必须构建自己的逻辑来处理错误、提交和验证检查是一件很烦人的事情？

假设我们构建了一个注册新用户的基本表单:

这里，我们有一个注册新用户的表单。用户可以输入他们的名、姓以及出生日期，还可以添加尽可能多的联系信息。

我们还有一个二级表单，允许用户设置他们的年龄和联系信息列表。在 secondaryForm 中，我们有一个 div 部分供用户设置年龄和联系信息列表。为了传入联系信息，我们将从父组件接收的联系数组和 setContact 传入联系组件。

![](img/b991f153e8cba32529c1b19ccf6ff8de.png)

Photo by [Greg Rosenke](https://unsplash.com/@greg_rosenke?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

嗯…为了让整个应用程序正常工作，我们真的需要进行道具训练吗？

输入 react-hook-form。

![](img/c93158c126f23190fb413df5b1198e9b.png)

Photo by [Matt Walsh](https://unsplash.com/@two_tees?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React-hook-form 是一个库，它允许我们构建一个需要更少代码的表单，并通过消除不必要的重新渲染来支持更好的性能。

嗯…少编码？怎么会呢？

为了理解这一点，让我们试着自己构建表单:

在这里，我们有一个由 secondaryForm 组成的 sampleForm，secondary form 由 ContactSection 组成。这与我们之前的内容相似，除了…

那些通过的道具都怎么了？

没错，react-hook-form 搞定了。在 react hook 表单中，所有字段都包装在 FormProvider 中，它为表单中的所有值提供上下文。

在 SampleForm 中，我们调用 useForm，它为表单中的所有值提供默认值，如名字、姓氏、年龄、联系人列表等。

在 secondaryForm 内部，我们可以调用 useFormContext 来访问 FormContext 中的其他可用字段，如 age。类似地，我们可以通过 useFieldArray 访问 contactInfo 列表，该列表被定制为从 formProvider 访问/编辑数组字段。

由于表单的其余部分可以访问表单上下文，因此不需要使用 prop drilling 在表单的不同部分之间传递状态变量。

当我们点击“提交”时，handleSubmit 被调用，onSubmit 作为回调被触发。在这个回调中，数据变量将包含 formContext 中的所有字段。

![](img/ab19a2d5ef02ea2064409f4b329a0802.png)

Photo by [Imad Alassiry](https://unsplash.com/@imadalassiry?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

恭喜你！您刚刚构建了您的第一个 React 钩子表单。

享受编码！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*