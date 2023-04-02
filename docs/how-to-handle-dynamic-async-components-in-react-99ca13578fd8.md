# 如何在 React 中处理动态和异步组件

> 原文：<https://javascript.plainenglish.io/how-to-handle-dynamic-async-components-in-react-99ca13578fd8?source=collection_archive---------7----------------------->

## 通过异步组件，我们可以向浏览器加载重要的和必不可少的组件。

![](img/14829c92dc741fb619657362db70ce69.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

异步不仅仅是获取数据，它还可以应用于代码或组件。通过异步组件，我们可以向浏览器加载重要的和必不可少的组件。不太重要的组件可以缓慢加载和渲染。在 React 中，这个概念是内置的，并为此提供了许多 API。

React 组件的延迟加载可以:

*   减少初始加载时间，
*   仅在需要时下载组件

React 的暂记 API 允许您处理 UI 中组件的异步加载。它让组件在渲染前“等待”一些东西。

# 1.React.lazy()的使用

`[React.lazy()](https://reactjs.org/docs/react-api.html#reactlazy)`允许您定义一个动态加载的组件。

要动态加载组件`LazyComponent.js`，我们需要动态导入并加载它，如下所示。

```
import { lazy } from 'react';
...
const LazyLoadComponent = lazy(() => import('./LazyComponent');
```

`React.lazy`仅支持默认导入。我们必须修改动态导入返回的承诺，使其具有命名导入的默认值。

```
const LazyLoadComponent = lazy(() => import('./LazyComponent')
  .then(
     module => ({ default: module.Content })
  )
);
```

动态导入和加载使组件不属于主捆绑包或代码块。因此，减少了初始页面加载。这样，我们可以根据组件是否很大、是否是初始渲染的一部分、对用户的可见性、是否是有条件渲染或者是否不太重要来划分组件。

# 2.React 的使用。焦虑

如果导入和加载量大、网络连接差、旧设备的处理时间长等，惰性加载组件可能需要等待一段时间。在这种情况下，我们需要提供一个后备 UI，向用户表明组件正在加载。这就是反应。悬念就来了。

`[React.Suspense](https://reactjs.org/docs/react-api.html#reactsuspense)`允许您指定加载指示器，以防其下树中的某些组件尚未准备好进行渲染。

```
import { lazy, Suspense } from 'react;
const Content = lazy(() => import("./Content"));export const AppComponent = () => (
   <Suspense fallback={<div>Loading...</div>}>
      <Content cost={COST} />
   </Suspense>
);
```

多个组件也可以嵌套在一个`Suspense`中。

# 3.交叉点观察器 API 的使用

做出反应。悬念 API 不支持惰性数据抓取。使用[交集观察者 API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) 我们可以在组件可见的情况下获取数据。这样我们可以在延迟加载的基础上再次减少加载时间，我们也可以延迟获取组件。我们也可以使用相同的原理为组件提供数据。

要使用交叉点观察器 API，我们可以创建如下观察器:

```
const options = {
  root: null,
  rootMargin: '750px',
  threshold: 1.0,
};const observer = new IntersectionObserver(callback, options);
observer.observe(targetElement);
```

我们也可以使用`[react-intersection-observer](https://www.npmjs.com/package/react-intersection-observer)` npm 包，它使用 API 来提供钩子、道具等。对于您的 React 应用程序。

阅读更多关于 React 应用程序代码分割的信息:

[](https://reactjs.org/docs/code-splitting.html) [## 代码分解-反应

### 大多数 React 应用程序会使用 Webpack、Rollup 或 Browserify 等工具“捆绑”文件。捆绑是一个过程…

reactjs.org](https://reactjs.org/docs/code-splitting.html) 

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*