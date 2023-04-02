# 使用 React Native 核心组件的 Todo 应用程序

> 原文：<https://javascript.plainenglish.io/todo-application-using-core-components-of-react-native-55079695fb12?source=collection_archive---------10----------------------->

## 通过创建 Todo 移动应用程序了解 React Native 的核心组件。

![](img/7cf76522566510fa85d56ecad720053f.png)

Image created by the author on Canva

React Native 提供了一系列基本的本地组件，可以用来开发我们自己的应用程序。这些内置组件被称为 React Native 的 ***核心组件*** 。许多核心组件包括视图、文本、图像、ScrollView、TextInput、样式表、按钮、SectionList 和 FlatList。

## 文本

文本是 React Native 的核心组件，用于显示支持嵌套、样式和触摸处理的文本。查看下面的示例代码来理解文本组件。这里，我们可以使用组件的 *style* 属性分配一个样式，而 *onPress* 提供触摸处理。我们也有文本中的文本，这被称为嵌套。

## 文本输入

这个核心组件允许用户输入文本。组件的 *onChangeText* prop 接受每次文本改变时调用的函数。另一个重要的道具是 *onSubmitEditing* ，它也有一个在提交文本时被调用的函数。

## 平面列表

该列表组件用于在滚动列表中显示不断变化但结构相似的数据。FlatList 最有助于处理长列表数据，其中许多项目会不时发生变化。它需要两个道具来显示数据: ***数据*** 和 ***renderItem。数据*** 是信息源，render item 一次只呈现一个项目。

## 章节列表

SectionList 也类似于 FlatList，除了它提供的逻辑节。如果您想将列表分成逻辑部分，每个部分都有标题，那么 SectionList 就是解决方案。比如我们手机上的联系人列表就是按字母顺序划分的。

## 视图

在任何 Android 或 iOS 移动应用程序开发中，视图都是用户界面的基本构件。一些视图中可以包含其他视图，这意味着整个应用程序都有视图。

## 安全区域视图

这也类似于一个视图组件，只是不同之处在于它只呈现设备安全区域边界内的内容。它是 iOS 的核心组件，因此目前仅在版本 11 或更高版本的 iOS 设备上受支持。

## 样式表

样式表是一种类似于 CSS 样式表的抽象。我们可以使用`StyleSheet.create`创建一个样式表，并将其存储在一个变量中，我们可以用这个变量来为组件分配样式。你可以从这里的[中学到更多关于这种风格的知识。](https://reactnative.dev/docs/stylesheet)

# 待办事项应用程序

让我们学习如何在我们的应用程序中使用这些核心组件。在这里，我使用核心组件开发了一个简单的 Todo 应用程序。如果你是初学者，需要帮助创建一个新的 React 原生项目，请点击下面的链接查看我的另一篇文章。

[](/getting-started-with-react-native-731d0a54c4b6) [## React Native 入门

### 开始学习跨平台移动应用程序开发

javascript.plainenglish.io](/getting-started-with-react-native-731d0a54c4b6) 

*   ***TextInput*** 组件用于在我们的应用程序顶部添加一个文本输入字段。此字段用于向待办事项列表添加项目。
*   ***视图*** 组件用于包含 ***文本输入*** 和我开发的另一个组件 ***TodoList*** 。
*   ***TodoList*** 组件返回一个***safea review***组件，其中包含 React Native 的核心组件 ***FlatList*** 。
*   ***FlatList*** 用于显示待办列表数组中的项目。每个项目都使用一个由 ***视图*** 组件包装的 ***文本*** 组件显示。每个组件的样式在文本组件中声明，样式取决于每个项目的***is completed****值。*

*使用以下代码开发您自己的 Todo 应用程序，并且不要忘记根据以下代码更改您的 App.js 文件。如果你想克隆我的项目，请访问我的库[这里](https://github.com/yagnikkardani/ToDoAppInReactNative)。*

# *结论*

*本文的目的是学习 React 本机基础知识及其核心组件。我还提供了一个示例 Todo 应用程序来理解 React Native 核心组件的用例。我希望这篇文章能帮助你学习 React Native 的核心组件。请跟随我阅读更多类似这样有趣的文章。*

*[](https://medium.com/@kardaniyagnik/membership) [## 通过我的推荐链接加入 Medium-Yagnik Kardani

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@kardaniyagnik/membership) [](https://www.buymeacoffee.com/kardaniyagnik) [## Yagnik Kardani 正在创建帮助他人成长的技术学习材料。

### 你好👋，我是一名媒体方面的技术作家。我喜欢学习并帮助他人在软件开发和云计算方面成长…

www.buymeacoffee.com](https://www.buymeacoffee.com/kardaniyagnik) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**