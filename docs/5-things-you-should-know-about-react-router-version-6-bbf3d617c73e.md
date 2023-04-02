# 关于 React 路由器版本 6 你应该知道的 5 件事

> 原文：<https://javascript.plainenglish.io/5-things-you-should-know-about-react-router-version-6-bbf3d617c73e?source=collection_archive---------6----------------------->

## 了解这个最常用和最重要的 React 包的最新版本中的重大变化。

![](img/c3e049238d565529a95b4f128f133a4a.png)

Photo by [Alexander Popov](https://unsplash.com/@5tep5?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 路由器版本 6 已于近日发布。这是一个非常大的变化。因为很多 React 项目都用 React 路由器。让我们看看版本 6 有什么变化。

**将** `**<Switch>**` **元素升级为** `**<Routes>**`

React 路由器版本 5，在使用 wrap 路由时支持`<Switch>`组件。

与 React 路由器版本 6 `<Switch>`不再支持。这是唯一的办法，那就是把`<Switch>`替换成`<Routes>`

`<Routes>`比`<Switch>`更强大

[了解更多信息](https://reactrouter.com/docs/en/v6/upgrading/v5#upgrade-all-switch-elements-to-routes)

**用** `**useNavigate()**` **代替** `**useHistory()**`

对于版本 5，当使用`useHistory()`时

```
const history = useHistory();We use for doing redirect, replace;history.push() or history.replace()
```

对于版本 6，我们不再使用`useHistory()`。我们用`useNavigate()`钩子代替`useHistory()`。

```
const navigate = useNavigate();We use for doing redirect, replace;navigate('/user');
navigate(-1); --> go abck previous page
```

如果您需要替换当前位置，而不是将新位置推送到历史堆栈上，请使用`navigate('/user', { replace: true })`

[了解更多信息](https://reactrouter.com/docs/en/v6/upgrading/v5#use-usenavigate-instead-of-usehistory)

**相对路线**

对于 React 路由器版本 5；

```
<Switch>
    <Route path='/'>
       <WelcomePage />
    </Route>
    <Route path='/user'>
       <UserPage />
    </Route>
</Switch>
```

这一变化是关于我们如何定义我们的路线。对于版本 5，路线有一个类似于孩子的`<WelcomePage />`或 `<UserPage />`。

对于版本 6，`<WelcomePage />`或 `<UserPage />`不会成为路由的子代。我们有了一个新的“元素”道具，而不是孩子。

```
<Routes>
   <Route path='/' element={<WelcomePage />} />
   <Route path="/users" element={<UserPage />} />
</Routes>
```

元素内部的值应该是 JSX 格式。

**CSS 类名**

```
<NavLink activeClassName={active} to='/person'>
```

对于第 5 版，一旦链接被激活，您可以使用该属性将一些 CSS 类自动应用到链接上。

对于版本 6，该道具被移除。如果想要应用一个激活的特定类，你必须手动查找这个链接是否激活。

```
<NavLink className={(data) => data.isActive ? active: ''} to='/person'>
```

**移除精确的**

```
<Route path='/user' exact element={<UserPage />}></Route>
```

对于版本 5，我们需要在这里添加 exact，因为，如果没有 exact，这将匹配以/user 开头的路径。

对于版本 6，确切的道具不见了，它总是寻找一个确切的匹配，如果你定义你的路径。

如果你想要只匹配路径开头的旧行为，你仍然可以通过在你的路径后添加 **/*** 来实现，当你添加时，如果 URL 路径以**/用户**开头，即使你这样做的原因是版本 6 内部有一个更好的算法来选择要加载的最佳路径。

```
<Route path='/user/userid' exact element={<Test/>}></Route>
<Route path='/user/selected' exact element={<Test/>}></Route>
```

对于版本 5，

```
<Route path='/test/testid' exact element={<Test/>}></Route>
```

路线总是赢

在版本 6 中，这种情况发生了变化，它在内部变得更加智能。您可以定义这两条路由，并访问选定的 react-router 查找。这里的最后一条路线是这条特定路径的最佳匹配。

```
<Route path='/user/userid' element={<Test/>}></Route>
<Route path='/user/selected' element={<Test/>}></Route>
```

对于版本 6，如果转到/选中，此；

```
<Route path='/user/selected' element={<Test/>}></Route>
```

该路由将通过路由器 6 建立。

[](https://bestte.medium.com/membership) [## 通过我的推荐链接加入 Medium—Beste

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

bestte.medium.com](https://bestte.medium.com/membership) [](/5-top-rated-q-a-for-angular-on-stack-overflow-bed610bf1c50) [## 5 堆栈上角溢出的顶级问答

### “这个项目从堆栈溢出开始”是开发人员如何开始她的故事。

javascript.plainenglish.io](/5-top-rated-q-a-for-angular-on-stack-overflow-bed610bf1c50) [](/how-to-work-with-the-angular-nebular-ui-library-and-use-a-simple-splash-screen-3dd0d1790478) [## 如何使用 Angular Nebular UI 库并使用简单的闪屏

### 闪屏在某些情况下是必要的，所以我想用一种非常简单的方式来展示它，我将谈谈…

javascript.plainenglish.io](/how-to-work-with-the-angular-nebular-ui-library-and-use-a-simple-splash-screen-3dd0d1790478) [](/how-to-use-sass-and-enjoy-css-with-dynamic-structure-900ea2adddf7) [## 如何使用 Sass，享受动态结构的 CSS

### 由于 CSS 是一个静态结构，我们必须不断重复代码。我们给 CSS 代码带来了动态结构…

javascript.plainenglish.io](/how-to-use-sass-and-enjoy-css-with-dynamic-structure-900ea2adddf7) [](/how-to-use-the-composition-api-to-get-data-from-service-with-vue-js-4da1eca19ad6) [## 如何使用组合 API 通过 Vue.js 从服务中获取数据

### 通过使用组合 API 而不是选项 API，可以使服务结构更加可用。

javascript.plainenglish.io](/how-to-use-the-composition-api-to-get-data-from-service-with-vue-js-4da1eca19ad6) 

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*