# 使用 Vue 路由器在 Vue.js 中的视图之间导航

> 原文：<https://javascript.plainenglish.io/navigation-between-views-in-vue-js-with-vue-router-2d890f0b0fb1?source=collection_archive---------9----------------------->

![](img/923077169ddf2aa707c0e89bd0e2685a.png)

在 Vue 中创建一个应用程序后，您通常会希望它由多个视图或页面组成。为此，我们需要使用一个名为`vue-router`的附加包。创建一个简单的 Vue 应用程序很容易，所以在本指南中，我们将看看如何将`vue-router`添加到您的新应用程序中。要首先创建您的应用程序，您只需运行以下命令:

```
npm i -g @vue/cli 
vue create my-app
```

然后，**添加一个路由器**到你的应用程序中，这样你就可以在页面间导航，也同样简单。也只需运行以下命令:

```
vue add router
```

可能会询问您是否要使用历史模式。如果你没有偏好，你可以输入`Y`。之后，您将在项目中获得更多的文件夹和文件。你的整体结构应该是这样的:

```
- public
--- favicon.ico
--- index.html
- src
--- assets
--- components
--- router
------ index.js
--- views
------ About.vue
------ Home.vue
--- App.vue
--- main.js
- package.json
- package-lock.json
```

如您所见，您现在有了许多路由器的新文件，以及对现有文件的一些更改。例如，在`main.js`中，您的应用程序将使用现在已经创建的路由器文件夹。`index.js`文件将被导入，如下所示:

```
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'createApp(App).use(router).mount('#app')
```

# 修改您的 Vue 路由器

在您的`/router/index.js`文件中，您将找到路由器的配置！您可以在这里设置页面。默认情况下，您会发现您的`router`看起来有点像这样:

```
import { createRouter, createWebHistory } from 'vue-router'
import Home from '../views/Home.vue'const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  }
]const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})export default router
```

所以添加路由有两种方式，如上图。您可以使用`import()`函数导入，或者使用典型的 JavaScript `import`语句导入`import`。每个`route`有 3 个不同的部分:

*   `path`，这是用户能够导航到的 URL。
*   页面的`name`，它是页面的标识符。
*   页面的`component`。这是当用户导航到`path`时将出现的组件。

```
{
    path: '/',
    name: 'Home',
    component: Home
}
```

要添加更多，你只需要添加更多到对象中——所以下面我添加了一个新的页面叫做`/contact-us`，使用了一个在`'../views/ContactUs.vue'`中找到的组件:

```
import { createRouter, createWebHistory } from 'vue-router'
import Home from '../views/Home.vue'const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/contact-us',
    name: 'ContactUs',
    component: () => import('../views/ContactUs.vue')
  },
  {
    path: '/about',
    name: 'About',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  }
]const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})export default router
```

# 使用 Vue 路由器的动态路由

这很好，但是如果你的 URL 端点不是静态的呢？例如，`/user/:id`，其中`:id`可以是任何东西。幸运的是，这也是可能的，只需以这种格式编写 URL 您只需在`path`属性中编写`/user/:id`:

```
{
    path: '/user/:name',
    name: 'User',
    component: () => import('../views/User.vue')
}
```

如果你使用过`express`，那么`vue-router`的匹配格式是熟悉的——事实上，你可以在`express`中进行任何路线匹配，你也可以在`vue-router`中进行。

# 使用 Vue 路由器重定向

**最后**，我们还可以设置一条路线重定向到另一条。您可以使用`redirect`属性来做到这一点。例如，下面将把`/home`重定向到`/homepage`:

```
{
    path: '/home',
    name: 'home',
    redirect: '/homepage'
}
```

这也可以定义为命名路由。下面，我们将把`/home`重定向到名称为`about`的路线:

```
{
    path: '/home',
    name: 'home',
    redirect: { name: 'about' }
}
```

最后，你也可以把它定义为一个函数..这意味着您可以创建一些更复杂的逻辑来处理重定向:

```
{
    path: '/user/:id',
    name: 'home',
    redirect: (to) => {
        // to will contain information about the route
        // to.params.id will be whichever `id` is in the URL in /user/:id
    }
}
```

# 使用 Vue 路由器在页面间导航

现在我们已经定义了我们的路由器，我们想在我们的应用程序中使用它。您可能会注意到您的`App.vue`文件略有变化，包含如下内容:

```
<template>
    <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
    </div>
    <router-view/>
</template>
```

`<router-link>`标签可用于在路由器`index.js`文件中定义的路由之间轻松导航。点击后,`<router-view>`标签将最终包含您的路线。不过，每条路由还将包含它们自己的`<router-view>`，这意味着您可以拥有嵌套路由。这些都可以在`/routes/index.js`中定义。例如，下面是一个嵌套路由，其中包含两个潜在的子路由`dashboard`和`posts`:

```
const routes = [
    {
        path: '/user/:name',
        name: 'User',
        component: import('../views/User.vue'),
        children: [{
            path: 'dashboard',
            component: import('../views/Dashboard.vue'),
        },
        {
            path: 'posts',
            component: import('../views/Posts.vue'),
        }]
    }
]
```

现在，既然我们已经定义了子组件，我们仍然可以使用`/user/:name`路径，但是现在有两个额外的组件将在`User.vue`中呈现，分别通过`/user/:name/dashboard`和`/user/:name/posts`访问。所以当`User`在 App.vue `<router-view>`中渲染时，`dashboard`和`posts`将在`<router-view>`的`User.vue`版本中渲染。它看起来有点像这样:

```
┌ - - - - - - - - - - - - - - - - - - ┐
| App.vue                             |
| ┌ - - - - - - - - - - - - - - - - ┐ |
| | User.vue                        | | 
| | ┌ - - - - - - - ┐ ┌ - - - - - ┐ | |
| | | Dashboard.vue | | Posts.vue | | |
| | └ - - - - - - - ┘ └ - - - - - ┘ | |
| └ - - - - - - - - - - - - - - - - ┘ |
└ - - - - - - - - - - - - - - - - - - ┘
```

这最终意味着当您导航到`/user/:name`时`User.vue`组件将始终可见，但是`Dashboard.vue`和`Posts.vue`组件只有在您导航到这些路线时才会可见！

# 使用 Vue 路由器的编程路由

就像我们如何使用`<router-link>`一样，我们也可以使用`router.push`以编程方式导航到一条路线。`<router-link to="/about">`同样可以用 JavaScript 写成这样:

```
router.push('/about')
```

如果我们想更高级一点，我们可以传入一个对象。例如，下面将以编程方式导航到定义为`About`的`name`路径，并在末尾添加一个查询字符串`?id=15`。如果`About`路由的`path`为`/about`，那么它将重定向到的 URL 将为`/about/?id=15`:

```
router.push({ name: 'About', query: { id : 15 }})
```

类似地，相同的 JavaScript 可以用 HTML 表示如下:

```
<router-link to="{ name: 'About', query: { id : 15 }}">About</router-link>
```

# 用 Vue 路由器防止后退按钮

**虽然**这将为用户导航添加一个新的历史记录条目，但我们也可以**为用户替换**当前页面——这意味着没有历史记录或返回上一页的按钮可用。这通常是不可取的，但在某些情况下会有一些有限的用途。为了以编程方式做到这一点，我们可以使用`router.replace`:

```
router.replace({ name: 'About', query: { id : 15 }})
```

或者在 HTML 中，追加`replace`属性:

```
<router-link to="{ name: 'About', query: { id : 15 }}" replace>About</router-link>
```

# 结论

我希望你已经喜欢这个指南开始使用 vue 路由器。Vue 中的路由器是设置一个新应用程序的一个非常重要的部分，它给了我们在 Vue 中定义和构建页面如此大的灵活性。要了解更多关于 Vue 的信息，请查看我的其他指南。