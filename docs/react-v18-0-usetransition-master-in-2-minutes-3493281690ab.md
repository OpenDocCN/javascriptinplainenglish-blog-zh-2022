# React 18 的 useTransition()钩子:2 分钟内掌握

> 原文：<https://javascript.plainenglish.io/react-v18-0-usetransition-master-in-2-minutes-3493281690ab?source=collection_archive---------4----------------------->

## 让我们快速了解一下，React 18 的 useTransition()钩子是什么，以及它将如何在 React 应用程序中发挥作用。

![](img/b221c72d7efafe0455957705acb1d76e.png)

Created by Author on [Pixlr](https://pixlr.com/x/#editor)

# React v18.0

React v18 是 React 的新发布版本，它引入了许多新功能，如自动批处理，新的 API 如`useTransition()`，以及新的流媒体服务器渲染器。现在，我们想成为`useTransition()`的主人，这是 React 增加的一个重要特性。

## 为什么需要 useTransition()。

为了回答这个问题，让我在这里创建一个假想的场景。考虑一个例子，有一个应用程序显示来自 API 的用户数据。我们有一个名为“Next”的按钮来加载 API 中下一个用户的数据。用户数据很大，完全加载需要时间。

现在，当我们按下“下一步”按钮时，当前页面数据将消失，我们会看到显示的加载信息。这对于应用程序用户来说是一种不愉快的体验。如果我们等到数据加载后再转换到新屏幕，那就太好了。

因此，React 在 React 版本 18 中引入了这个新的`useTransition()`钩子。此挂钩的导入语句和声明:

```
import { useTransition} from "react"; // Import Statement
const [isPending, startTransition] = useTransition(); //Declaration
```

*   **isPending:** 是一个布尔值。它的值告诉我们此时转换是否正在发生。对于正在进行的转换为真，否则为假。
*   **startTransition:** 是一个函数，用于通知 React 我们想要延迟哪个状态更新。

## 例子

我们用一个简单的例子来理解一下`useTransition()`的清晰概念。这里，我们有一个从大型免费 API 打印图像的应用程序。当我们最初启动应用程序时，显示会很清晰。

我们有一个名为' ***'的按钮，它调用一个名为`loadData()`的函数，它被包装在`startTransition`函数中。这是我们告诉 React 我们不介意等待该函数完成加载数据的方式。一旦完成加载数据，它会将' ***isPending*** '的值设置为 False。***

loadData 函数从 API 获取图像数据，并将其设置为名为' ***images*** '的状态变量。然后，我们将*图片*作为道具传递给另一个名为“***display images***”的组件，它将在那里显示图片。

为了生成整个效果，我将 *DisplayImages* 组件包装在一个 div 中，并将不透明度设置为 0.5，直到 *isPending* 变为 False。

Example: useTransition() Hook

在这里，我已经添加了沙盒链接，如果你想玩代码，并了解它是如何工作的。只需点击它，并在沙盒上测试应用程序。

Code in Sandbox Link

# 结论

本文的目的是理解 React 版本 18 的`useTransition()`钩子，以及如何在 React 应用程序中使用它。我已经尽力用一种简单可行的方式向你解释清楚了。如果你有任何问题，请写在评论区，我会尽一切可能帮助你。如果你喜欢我的文章，请关注我并保持更新。

[](https://medium.com/@kardaniyagnik/membership) [## 通过我的推荐链接加入 Medium-Yagnik Kardani

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@kardaniyagnik/membership) [](https://www.buymeacoffee.com/kardaniyagnik) [## Yagnik Kardani 正在创建帮助他人成长的技术学习材料。

### 你好👋，我是一名媒体方面的技术作家。我喜欢学习并帮助他人在软件开发和云计算方面成长…

www.buymeacoffee.com](https://www.buymeacoffee.com/kardaniyagnik) 

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*