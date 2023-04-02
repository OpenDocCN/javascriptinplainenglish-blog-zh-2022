# React Hooks — useMemo() —通过示例进行说明

> 原文：<https://javascript.plainenglish.io/quickly-learn-usememo-hook-2fb59fd99b62?source=collection_archive---------5----------------------->

## 什么是 useMemo()？我们应该什么时候使用它？怎么用？

![](img/f82564d31fad20e718cb808468928bb8.png)

Image created by Author on [Pixlr](https://pixlr.com/x/)

## 什么是 useMemo()？

*useMemo()* 钩子与 useCallback()非常相似。它将一个函数和一组依赖项作为参数，并返回一个记忆值，只有当其中一个依赖项发生变化时，该值才会重新计算。如果没有提供数组，每次渲染都会计算一个新值。参见下面的声明:

```
const result = useMemo(() => computeExpensiveValue(counter1), [counter1]);
```

## 我们应该什么时候使用它？

useMemo()钩子的目的是停止一些昂贵函数的不必要的运行。简单地说，只有当其中一个依赖项(作为 useMemo 的第二个参数传递)发生变化时，由 useMemo()钩子包装的函数才会运行。

考虑两个计数器(*计数器 1* 和*计数器 2* )和一个具有一些昂贵(即耗时)计算的函数的简单例子。我们的函数(`*computeExpensiveValue(counter1)*`)使用 *counter1* 的值来生成昂贵的值。因此，我们的函数在 *counter1，*改变时重新计算昂贵的值，这是正常的。但是，它也会根据*计数器 2、*的变化重新运行，这是完全不必要的。我们称之为应用程序的低性能。因此，无论何时您在应用程序中遇到任何类似的问题，您都应该考虑将您的函数包装在 *useMemo()* 钩子中。

让我们用两个不同的例子来理解它，不用 useMemo 和用 useMemo。我还添加了两种情况下的输出，因此您可以看到它们之间的区别。

## 案例 1:没有使用备忘录()

## 输出:

Output Video created by Author

## 案例 2:使用 useMemo()

## 输出:

Output Video created by Author

# 结论

本文的目的是理解 React 的 useMemo()钩子。我已经用一个简单的反例解释了钩子的用例。每个案例所附的视频旨在展示它们之间的差异。我希望这篇文章能帮助你理清 useMemo()钩子的概念。但是，如果你有任何疑问，请在评论中写下来，我会尽力帮助你。感谢阅读我的文章，如果你喜欢我的文章，请关注我，保持更新。

[](https://medium.com/@kardaniyagnik/membership) [## 通过我的推荐链接加入 Medium-Yagnik Kardani

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@kardaniyagnik/membership) [](https://www.buymeacoffee.com/kardaniyagnik) [## Yagnik Kardani 正在创建帮助他人成长的技术学习材料。

### 你好👋，我是一名媒体方面的技术作家。我喜欢学习并帮助他人在软件开发和云计算方面成长…

www.buymeacoffee.com](https://www.buymeacoffee.com/kardaniyagnik) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*