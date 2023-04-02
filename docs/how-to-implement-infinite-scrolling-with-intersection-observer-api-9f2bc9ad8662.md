# 如何用交集观察者 API 实现无限滚动

> 原文：<https://javascript.plainenglish.io/how-to-implement-infinite-scrolling-with-intersection-observer-api-9f2bc9ad8662?source=collection_archive---------2----------------------->

## 通过使用交叉点观察器 API 实现更简单、性能更好的无限滚动

![](img/ec7859bc7a18a1f1ccf5d6eaf9eca223.png)

Photo by [Taylor Wilcox](https://unsplash.com/@taypaigey?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

当我们的列表页面有很多数据，比如 200 个条目，但我们不能一次请求所有数据，因为请求会很慢，这将导致糟糕的体验。通常，我们会对数据进行分页，每个分页可能包含 10 项。我们将只加载前 10 个项目，当需要浏览更多的项目，接下来的 10 个项目将被加载。

在移动页面上，无限滚动是一种非常常见的分页方式。由于传统的分页模式，更多的数据只有在用户点击之后才被加载。无限滚动允许用户在滚动到页面底部时自动加载更多内容，无需任何额外操作，体验更好。

在本文中，我们将通过使用[交叉点观察器 API](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver) 实现无限滚动。

# 如何实施

我们将分两步实现无限滚动:

1.  用 JavaScript 生成一个列表。
2.  使用交叉点观察器 API 加载更多内容。

## 用 JavaScript 生成列表

首先，我们生成一个空白列表页面，然后通过 JavaScript 的 setTimeout 模拟一个请求来加载数据，最后将数据呈现到页面上。

## 使用交叉点观察器 API 加载更多内容

交叉点观察器 API 可以观察一个元素是否可见，所以当用它来完成无限滚动时，需要在列表底部添加一个元素。当元素可见时，加载更多内容。

在`ol`旁边添加一个`div`元素:

```
<ol class="list"></ol>
<div class="more">loading</div>
```

然后使用交叉点观察器 API 观察元素，当元素可见时，加载接下来的 10 项:

```
const intersectionObserver = new IntersectionObserver(entries => {
  if (entries[0].intersectionRatio <= 0) return;
  // load more content;
  loadItems(10);
});
// start observing
intersectionObserver.observe(document.querySelector(".more"));
```

用交叉点观察器 API 做无限滚动就是这么简单。不过这个实现会有一个小的体验问题。只有当用户看到`loading…` 元素时，数据才会被加载。如果数据是在用户从页面底部再向前滚动一点时加载的，那就太好了。

我们可以通过添加一个占位符元素来优化它，让观察者提前执行。

```
<ol class="list"></ol>
<div class="more">
  <p class="virtual"></p>  // and a placeholder element
  loading ...
</div>
```

添加一些样式以确保占位符元素不会影响列表的显示:

```
.virtual {
  position: absolute;
  height: 200px;
  top: -200px;
  width: 100%;
  pointer-event:none;
}
```

您可以通过 CodePen 上的以下示例来体验它:

# 结论

无限滚动也可以通过监听滚动事件来实现，但是我们必须不断计算滚动位置。而使用交集观察者 API，只需要提供一个回调函数，当目标元素进入视区时，就会自动执行，不仅简单而且性能更好。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*