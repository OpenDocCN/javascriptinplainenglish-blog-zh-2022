# Next.js 中应该用 Redux 吗？

> 原文：<https://javascript.plainenglish.io/should-you-use-redux-in-next-js-5e57201c34da?source=collection_archive---------0----------------------->

## 你真的需要吗？

![](img/2f3eafcb48ac24acb2c3dda7452fd933.png)

Photo by Andrea Piacquadio: [https://www.pexels.com/photo/man-in-red-polo-shirt-sitting-near-chalkboard-3779448/](https://www.pexels.com/photo/man-in-red-polo-shirt-sitting-near-chalkboard-3779448/)

Redux 是 React 应用程序中状态管理的绝佳选择。但它也受到了相当多的批评。

围绕**的任何问题都很难回答，因为在大多数情况下，答案是:**

***看情况…***

但是今天，我将尝试回答我们是否应该在 Next.js 中使用 Redux 的问题，并向您展示一些您可能想要考虑的替代方法。

# 我的直接回答

如果你想知道我对这个话题的直接看法，答案是:

***你真的应该尽量避免在 Next.js 中使用 Redux***

我来解释一下原因。

Redux 最初是为了在复杂的组件层次结构之间共享公共状态而发明的。

# 原因一:Next.js 架构不适合 Redux。

Next.js 应用程序的一般架构通常与 React 应用程序非常不同。

在`NextJS`中，我们有`**getServerSideProps**`和`**getStaticProps**`的概念，它们可以在渲染之前填充页面所需的数据。

所以在 Next.js 中使用 Redux 往往没有那么大意义。

# 原因二:Redux 有其他替代方案。

React 现在支持上下文，可以在组件之间共享公共状态。

如果您有许多需要共享数据的嵌套组件，那么您可以只使用`React Context`。像下面这样:

useContext.ts

在许多情况下，您甚至不需要任何集中式状态管理解决方案。我今天也会展示这一点！

# 原因三:设置起来非常非常复杂。

了解了所有这些之后，如果您仍然觉得在您的 Next.js 应用程序中需要 Redux，请注意

***用 Next.js 设置 Redux 真的很复杂***

你需要一个名为`[next-redux-wrapper](https://github.com/kirill-konshin/next-redux-wrapper)`的特殊包来让它工作。即使在这之后，处理服务器和客户机状态并使它们同步也是一件非常痛苦的事情。点击此处了解更多信息:

[](https://github.com/kirill-konshin/next-redux-wrapper) [## GitHub-kiri ll-kon shin/next-redux-wrapper:next . js 的 Redux 包装器

### 一个将 Next.js 和 Redux 结合在一起的特设库⚠️这个库的当前版本只适用于 Next.js 9.3 和…

github.com](https://github.com/kirill-konshin/next-redux-wrapper) 

# 原因 4:在 Next.js 中优化 Redux 比较复杂。

即使在所有这些之后，如果您设法将 Redux 与 Next.js 集成，您将面临的下一个问题是性能。

反对 React 上下文的一个重要理由是它的性能影响。使用 Redux 有时可以通过使用选择器解决这个问题。

useSelector.ts

嗯，在 Next.js 里很难做到。

我并不是说这是不可能的，但是为了 Next.js 的性能而适当地优化 Redux 可能会非常困难，并且需要很长的时间。

# 好吧，但我有什么选择？

很高兴你问了；我并不是说你不应该在 Next.js 应用程序中使用 Redux。

我想说的是，

***问问自己是否真的需要 Redux。***

我将展示一些场景，在这些场景中，您可能会认为 Redux 是一条可行之路，但实际上还有更好的替代方案。

我们去探险吧，好吗？

## 场景 1:你已经知道页面上的内容。

假设您正在构建一个电子商务应用程序，其中大多数 URL 都是预先确定的。

在普通的 React 应用程序中，我们可能会想到获取产品的详细信息，并将其保存到 Redux 状态并显示在页面上，但在 Next.js 中，有一种更好的方法可以做到这一点:

```
/products -> Shows the list of the product/product/{productId} -> Shows the details of the product
```

因此，如果你知道用户将访问某个页面，`**/product/{productId}**`，那么你甚至在加载页面之前就已经知道了`**productId**`。

您可以直接预取数据，预先生成页面，然后发送给访问者，从而提高应用程序的性能。

在这些情况下，您可以使用`**getStaticProps**`,因为您已经知道页面上会有什么数据。它也有助于缓存！

getStaticProps

如果产品列表随时间变化，可以使用`**getServerSideProps**`代替此功能。

getServerSideProps

所以[如果你在加载实际页面之前就知道页面上会呈现什么数据](https://medium.com/p/dadabf45e562)，那么你就可以像老板一样使用`**getStaticProps**`和`**getServerSideProps**`来完成工作。

## 场景 2:你不知道接下来会发生什么

这是大多数实际应用程序中非常常见的场景。我们可能知道初始页面加载时会出现什么，但是页面的内容取决于用户的操作。

带有分页的产品页面就是一个很好的例子。所以你只知道在第一页加载什么。但是在初始页面加载后，用户可能希望看到下一个页面。

比如亚马逊网站上的以下分页:

![](img/5706f5e88feafe4774f64073166ed909.png)

Amazon’s Pagination Component

在这种情况下，使用静态生成很棘手，因为您必须获取新数据。这种情况下应该用 redux 吗？

答案是否定的。使用类似于`[**swr**](https://swr.vercel.app/)`或`[**react-query**](https://react-query.tanstack.com/)`的查询库来管理 API 数据会更好。

下面是一个使用[**react-query**](https://tanstack.com/query/v4/docs/guides/paginated-queries)**:**的例子

usePaginatedQuery.ts

那么，当您可以在不使用 redux 的情况下获得缓存和预取等令人惊叹的功能时，为什么还要获取数据并将其存储在 Redux 存储中呢？

## 场景 3:您需要在组件之间共享一些公共状态。

假设您的应用程序有某种身份验证设置。在这种情况下，您会希望在组件之间共享身份验证状态。也许是为了显示和隐藏登录按钮。

***你现在做什么？***

你可能会想，好吧，那么现在我需要使用 Redux 在任何地方共享认证状态。

嗯，事实上，没有。

如果你正在处理这样简单的场景，你可以利用好的旧浏览器`**LocalStorage**` **。**也许可以用一个漂亮的小挂钩把它包起来:

useAuthState.ts

如果`**Localstorage**`对你来说不是一个选项，那么你应该试着先设置`R**eact Context**`。

但是不要误解我。

Redux 将在这里完美地工作。但是你应该首先考虑使用 React Context API，它是 React 自带的，可以节省宝贵的包大小！

而且设置起来也比较容易！

## 你还有其他一些用例吗？

在所有这些之后，您仍然有一个特定的用例，其中您需要在您的组件之间共享一个公共状态，然后使用 Redux。

只是不要急于求成。试着先理解你为什么需要它，然后正确地使用它，这样它不会比解决你已经有的问题产生更多的问题！

## 最后的想法

我希望你今天学到了新东西。祝您愉快！:D

```
**Want to Connect?**You can reach out to me via [**LinkedIN**](https://www.linkedin.com/in/56faisal/) or my [**Personal Website**](https://www.mohammadfaisal.dev/blog)
```

[](/advanced-testing-setup-for-an-enterprise-react-project-a182cc74c749) [## 企业 React 项目的高级测试设置

### React 测试库、Redux、路由器等用例

javascript.plainenglish.io](/advanced-testing-setup-for-an-enterprise-react-project-a182cc74c749) [](/how-to-animate-the-page-transition-in-next-js-68c7b888dce3) [## 如何在 Next.js 中制作页面过渡动画

### 仅用五行代码在 Next.js 中制作页面转换动画。

javascript.plainenglish.io](/how-to-animate-the-page-transition-in-next-js-68c7b888dce3) [](/how-to-show-loader-on-page-changes-in-next-js-102edd0ec98d) [## 如何在 Next.js 中显示页面变化的加载器

### 让你的用户参与一个伟大的视觉反应！

javascript.plainenglish.io](/how-to-show-loader-on-page-changes-in-next-js-102edd0ec98d) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。**