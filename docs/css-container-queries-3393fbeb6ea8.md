# CSS 容器查询

> 原文：<https://javascript.plainenglish.io/css-container-queries-3393fbeb6ea8?source=collection_archive---------1----------------------->

## *什么是容器查询，它们解决了哪些问题？*

![](img/8e0fd872a381afee1a78fd347e0b76d0.png)

Photo by [CHUTTERSNAP](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

CSS 容器查询将于 2022 年 8 月 30 日登陆 Chrome。这使得 Chrome 成为第一个在其稳定版本中实现期待已久的功能的浏览器。Safari 可能会在今年晚些时候推出。Safari 16 预览版中已经有了。不幸的是，我找不到关于 Firefox 的信息，所以如果你知道他们的计划，请在评论中告诉我们。

如果你要开始一个新的项目或者编写一个新的设计系统，并且迫不及待地想要使用容器查询，你可能想要利用一个 poly fill([https://github . com/Google chrome labs/Container-query-poly fill](https://github.com/GoogleChromeLabs/container-query-polyfill))。

这里是 caniuse 页面的链接，这样你就可以跟踪浏览器的兼容性:[https://caniuse.com/?search=Container%20Queries](https://caniuse.com/?search=Container%20Queries)

## CSS 中的容器查询是什么？

容器查询是“本地媒体查询”，应该用于微布局(单个组件的自包含布局)。

想象一下，你正在设计一个带有长文本的按钮，并且你在你的网站的多个地方重复使用这个按钮。目前，您可能会像这样使用媒体查询:

```
@media (max-width: 420px) {
  .button {
    ...
  }
}
```

问题是该查询依赖于当前视口的宽度。你不知道保存按钮的容器有多宽。

将来，你会写出这样的东西:

```
@container (width < 420px) {
  .button {
    ...
  }
}
```

与媒体查询相比，容器查询取决于元素可用的实际大小。

## 如何使用 CSS 容器查询？

这里有一个简单的代码示例来理解容器查询:

```
div {
  **container-type: inline-size;**
  width: 20%;
}.button {
  padding: .5rem 1rem;
  border: 0;
  background: rebeccapurple;
  color: #fff;
}[**@container**](http://twitter.com/container) **(width < 120px)** {
  .button > span {
     display: none;
  }
}
```

(这是一个骗局，目前只在 chrome 预览版中工作，或者在 Chrome 中激活标志“容器查询”和“实验性网络平台功能”时://flags/:[https://jsfiddle.net/Lr081cn9/](https://jsfiddle.net/Lr081cn9/))

我强调了两行:

我们必须在父元素上设置容器类型。第一个突出显示的行是父 div 上的一个属性(我们的按钮是这个元素的子元素)。容器类型告诉 CSS 应该查询哪个属性。在这种情况下，它是宽度(因为宽度决定了元素的行内大小)。

`container-type`的其他可能值有:

*   大小-内联查询和块大小。
*   样式(默认)—查询特定的样式(可用于查询黑暗模式、辅助功能支持等)

可用的容器类型可能取决于使用的浏览器/聚合填充。不幸的是，规范还没有完成，所以这是可以改变的。您可能会读到其他容器类型，如`state`或`block-size`，但它们已经从规范中删除了**(预计它们将在规范的未来版本中再次添加)。旧的聚合填充可能仍会实现它们。**

**突出显示的第二行是实际的查询。这看起来像一个媒体查询，但是我使用了新的范围语法。我写了另一篇关于语法的文章，也将很快提供给媒体查询！您可以在这里找到它:**

**[](/new-css-media-query-range-syntax-2b41fab34fa5) [## 新的 CSS 媒体查询范围语法

### 新语法于本月早些时候登陆 Chrome

javascript.plainenglish.io](/new-css-media-query-range-syntax-2b41fab34fa5) 

## 容器可以被命名

除了我之前提到的最简单的用例，容器查询还提供了命名容器。看一下下面的例子:

```
div {
  container-type: inline-size;
  **container-name: my-sidebar;**
  width: 20%;
}.button {
  padding: .5rem 1rem;
  border: 0;
  background: rebeccapurple;
  color: #fff;
}[**@container**](http://twitter.com/container) **my-sidebar (width < 120px)** {
  .button > span {
     display: none;
  }
}
```

之前，我们查询了每个容器类型为`inline-size`的容器。在这种情况下，我们只查询类型为`inline-size`和名称为`my-sidebar`的容器。

## 容器查询速记语法

和许多其他 CSS 属性一样:容器查询有自己的简写语法。`container`属性只需要名称和类型，用正斜杠分隔:

```
div {
  **container: my-sidebar / inline-size;**
  width: 20%;
}.button {
  padding: .5rem 1rem;
  border: 0;
  background: rebeccapurple;
  color: #fff;
}[**@container**](http://twitter.com/container) **my-sidebar (width < 120px)** {
  .button > span {
     display: none;
  }
}
```

就这些了，伙计们！

容器查询是一个相对简单的功能，类似于大多数部件的媒体查询。** 

***更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*****