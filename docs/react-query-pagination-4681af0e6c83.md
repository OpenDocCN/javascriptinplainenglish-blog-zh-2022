# React 查询分页

> 原文：<https://javascript.plainenglish.io/react-query-pagination-4681af0e6c83?source=collection_archive---------8----------------------->

## 易于添加的分页

![](img/a0490ab42b20a650687070f1dca90b2d.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 页码

分页是一种以更智能的方式处理网站性能的常用技术。现在，我们经常提供无限滚动分页，这意味着一旦用户滚动到底部，新的数据就会被获取或分页。

我在我的网站 [iHateReading](https://ihatereading.in/) 上添加了这种分页技术。我使用的技术栈是用于 API 调用和数据缓存的 react-query。

我也使用过[浏览器接口 API](https://dev.to/shreyvijayvargiya/intersection-observer-api-1901) 。这个 API 主要帮助浏览器跟踪和检测独占的 DOM 元素位置。交叉点 API 有助于跟踪 DOM 元素的位置，并在超过阈值时调用回调方法。

# 真实世界的例子

*   假设我们在长长的博客列表的最底部有一个“加载更多”按钮。
*   “加载更多”按钮被按下或出现在视图中，我们将使用 API 获取新数据

交集 API 基本上帮助我们跟踪 load more 按钮视图，并在交集时调用回调方法。

# 反应查询

React query 是一个钩子的集合，有助于在前端缓存和获取数据。我不会深入研究 react-query 的细节，因为我已经讲述了很多关于它的故事。

[React 查询短裤介绍](https://studio.youtube.com/video/QW9514m5dlI/edit)

[React 查询文章](https://medium.com/codex/3-steps-to-quickly-start-with-react-query-a3012c62b18b)

# 如何添加分页

让我们将方法分为两个阶段，一个是 API 调用，另一个是分页或页码。

**获取数据的 API 调用**
API 调用将从数据库中获取元素的页码。例如，第一页将获取 10 个项目，然后页码= 2 将从第 11 个项目到第 20 个项目获取项目，依此类推。

```
const {data, isLoading } = useQuery(["blogs"], 
 async() => { 
  const data = await fetchBlogs(pageNumber);
  return data;
 }
);
```

**页码**
页码由 UI 跟踪维护。一旦用户到达 load more 按钮，intersection API 将调用回调方法，并将页码增加 1。这种情况一直持续到页码达到最后一个值。

```
const [pageNumber, setPageNumber] = useState(0);
const [isIntersecting, setIntersecting] = useState(false);
const observer = new IntersectionObserver(([entry]) =>
 setIntersecting(entry.isIntersecting));useEffect(() => {
 observer.observe(ref.current);
   return () => observer.disconnect();
}, []);
```

**API 获取分页数据**

*   一旦我们点击“加载更多”按钮,`isIntersection`状态将变为真
*   交叉点 API 的回调函数将得到，并且页码值将增加 1。
*   `useQuery`将再次调用通过传递更新的 pageNumber 值来调用`fetchBlogs`方法的 API 调用。因此，我们的分页数据或接下来的 10 个项目将被提取。React query 将自动缓存这些新数据，以提供更好的用户体验并减少 API 调用的数量。

# 结论

这很容易使用 react-query 和 intersection API 来实现。否则，我们将不得不在每次用户滚动网页时跟踪 load more 按钮的位置，然后增加页码并再次调用 API 来获取接下来的 10 个项目。
变得有点混乱，性能也会受到阻碍，但通过使用反应查询和交集 API，我们避免了不必要的重新渲染，提高了应用程序的性能。

**继续发展
Shrey** [**IHA tereading**](https://ihatereading.in/)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***