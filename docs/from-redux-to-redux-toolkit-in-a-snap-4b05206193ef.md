# 从 Redux 到 Redux 工具包

> 原文：<https://javascript.plainenglish.io/from-redux-to-redux-toolkit-in-a-snap-4b05206193ef?source=collection_archive---------18----------------------->

## 我很容易地更新了一个 React Redux 代码库

![](img/209bfc2bb559b65535006aa87a508e5f.png)

Photo by [jom jakkid](https://unsplash.com/@jomer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/snap?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Redux 是 React 广泛使用的状态管理库，有助于保持应用程序代码的整洁。

第一次发布可以追溯到 2015 年，从那以后它就随着 React 逐渐改进。值得一提的一个重大改进是引入了 React 挂钩，而不是使用 React 类组件。

今天，React Redux 开发人员可以比以往任何时候都更容易地编写单页应用程序(spa)。

截至 2022 年，React Hooks 和 Redux 绝对是创建单页面应用的好方法，但还有更多。如果你想进一步用最简单的方式编写 Redux 应用程序，你可以看看 Redux Toolkit。

这正是我所做的。

顾名思义，Redux Toolkit (RTK)为您提供了创建 React Redux 应用程序通常需要的现成工具集，其中包括 Redux DevTools 扩展以及中间件和 thunk 函数。

不要错过了解更多内容的机会。

[](https://redux.js.org/introduction/why-rtk-is-redux-today) [## 为什么 Redux Toolkit 是今天如何使用 Today | Redux

### Redux Toolkit(也简称为“RTK”)是我们官方推荐的编写 Redux 逻辑的方法。的…

redux.js.org](https://redux.js.org/introduction/why-rtk-is-redux-today) 

但不仅如此，在我看来更有趣的是 Redux Toolkit 还附带了一系列关于如何正确编写代码的指南。

[](https://redux.js.org/faq/code-structure) [## 代码结构| Redux

### 由于 Redux 只是一个数据存储库，它对如何构建您的项目没有直接的意见。

redux.js.org](https://redux.js.org/faq/code-structure) 

如果你已经熟悉 Redux，你可能知道一切都可以归结为将你的代码组织成`actionTypes`、`actions`和`reducers`，它们通常保存在单独的文件和文件夹中。虽然这是一个非常有效的方法，但 ducks 模式允许将这三个部分写在一个名为 slice 的文件中。因此，样板代码的数量显著减少。

[](https://github.com/erikras/ducks-modular-redux) [## GitHub-Erik ras/ducks-modular-redux:捆绑减速器、作用类型和作用的建议…

### 我发现当我构建 redux 应用程序时，一次一个功能，我一直需要添加{actionTypes…

github.com](https://github.com/erikras/ducks-modular-redux) 

在这篇文章中，我不会详细讲述如何用 Redux Toolkit 编写 React Redux 应用程序。让我向你展示我是如何更新 [Redux Chess](https://github.com/chesslablab/redux-chess) 代码库，以遵循 Redux Toolkit 的最佳软件开发实践的。

我不得不说这比我原先预期的要容易。

# 让我们开门见山吧

我做的第一件事是安装 RTK。

```
$ npm i [@reduxjs/toolkit](http://twitter.com/reduxjs/toolkit)
```

然后，我写了下面这个`src/store.js`文件。

```
import { configureStore } from '@reduxjs/toolkit';
import rootReducer from './reducers/rootReducer';const store = configureStore({
  reducer: rootReducer,
});export default store;
```

很简单，不是吗？

如前所述，Redux Toolkit 开箱即用，提供了一套方便的工具来帮助您设置 Redux store:Redux dev tools 扩展、中间件等等。

因此，基本上我不得不将`createStore`替换为`configureStore`。

另一方面，这意味着也要从我的`src/reducers/rootReducer.js`文件中删除`combineReducers`助手函数，因为现在有了 Redux Toolkit，`configureStore`函数会自动调用`combineReducers`。

```
import boardReducer from './boardReducer';
import historyReducer from './historyReducer';...import gameTableReducer from './gameTableReducer';
import watchDialogReducer from './watchDialogReducer';const rootReducer = {
  board: boardReducer,
  history: historyReducer,...gameTable: gameTableReducer,
  watchDialog: watchDialogReducer
};export default rootReducer;
```

基本上就是这样！

当然，不要忘记做一些清理工作，并删除未使用的包，在我的情况下，这些包如下所述。

```
$ npm uninstall redux redux-devtools-extension redux-thunk
```

从那时起，我能够一点一点地开始重构过程。

最后，根据推荐的文件夹结构，将`src/reducers/rootReducer.js`移至`src/app/rootReducer.js`并将`src/store.js`移至`src/app/store.js`。

关于 Redux Chess 如何更新以遵守使用 Redux Toolkit 的最佳实践的更多细节，您可能想点击下面的 PR 链接。

[](https://github.com/chesslablab/redux-chess/issues/317) [## 使用 Redux Toolkit 问题#317 更新代码库以遵循最佳实践…

### 应该更新代码库，以遵循 Redux Toolkit 的最佳软件开发实践。现代 Redux 确实…

github.com](https://github.com/chesslablab/redux-chess/issues/317) 

非常感谢您的阅读，祝您学习和编码愉快。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***