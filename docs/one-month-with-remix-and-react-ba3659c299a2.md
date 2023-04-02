# 我花了 30 天时间尝试这个新的 React 框架

> 原文：<https://javascript.plainenglish.io/one-month-with-remix-and-react-ba3659c299a2?source=collection_archive---------2----------------------->

![](img/86d237dffcf9577ddbab8216e4e40b17.png)

Photo by [Lautaro Andreani](https://unsplash.com/es/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

混音现在是热门话题，但它值得大肆宣传吗？为了找到答案，我决定在我的下一个项目中尝试一下。

首先，它非常直观。我以前从未使用过全栈 web 框架，我甚至不用看文档就能创建基本的应用程序框架。

此外，我喜欢混音没有重新发明轮子的事实。它使用标准的 web API(fetch、WebCrypto)和普通的 HTML 表单与后端进行通信。最后，它无处不在！我能够毫不费力地在 Cloudflare Pages (Miniflare)上部署我的应用程序。

在这篇文章中，我将告诉你我使用这个框架的经历:这是我在使用 Remix 的第一个月中所发现的。

## 反应+混音= ❤

React 非常容易学习。混音非常容易学习。结合起来，它们是以光速构建全栈 web 应用的完美匹配。您只需要一个 React 组件、一个 HTML 表单和两个后端函数。

登陆页面上的例子已经告诉了你 90%你需要知道的东西。29 行代码解释了整个框架。

```
export async function loader({ request }) {
  return getProjects();
}

export async function action({ request }) {
  const form = await request.formData();
  return createProject({ title: form.get("title") });
}

export default function Projects() {
  const projects = useLoaderData();
  const { state } = useTransition();
  const busy = state === "submitting";

  return (
    <div>
      {projects.map((project) => (
        <Link to={project.slug}>{project.title}</Link>
      ))}

      <Form method="post">
        <input name="title" />
        <button type="submit" disabled={busy}>
          {busy ? "Creating..." : "Create New Project"}
        </button>
      </Form>
    </div>
  );
}
```

尽管编写页面可能非常容易，但极度的简单可能会让您的 React 组件陷入混乱。

正如我在上一篇文章中所写的，React 及其缺乏支持的设计模式增加了编写不一致代码的机会。因为所有的东西都写在一个文件里(HTML，JS，CSS，用 JS 写的 CSS，…)，所以要保持组件的整洁和简单需要付出更多的努力。除此之外，现在用 Remix 添加后端逻辑，这变得更加难以维护。

[](https://levelup.gitconnected.com/i-changed-my-mind-on-react-js-4ecf4b73e14) [## 我改变主意了。射流研究…

### 我不喜欢 React，我以前从来没用过。只是从外面看，我以为它没有…

levelup.gitconnected.com](https://levelup.gitconnected.com/i-changed-my-mind-on-react-js-4ecf4b73e14) 

利用嵌套路径和受控组件构建您的 web 应用程序。为了保留一个可读的代码库，我试图将 React 组件强制在 150/200 行(代码和 HTML)以下。这不是最终的解决方案，但结合良好的实践和坚实的原则，它可以给你很好的“意大利面条代码”红色信号。

## 一次编写，随处运行

Remix 应用程序可以“编译”为任何类型的平台，只需很少的代码更改。从您自己的定制服务器到 AWS、Vercel、Fly、Netlify 和 Cloudflare。

在开发期间，我制作了一些脚本来调试 Node 和 Miniflare 上的相同代码。由于 Cloudflare 页面的构建速度较慢，我更喜欢在 Node 中提供开发应用程序。有了 LiveReload，我可以更快地迭代我的 UI/UX 想法(特别是如果你使用 Tailwind CSS 的话)。

## 可能会很贵

我还没有在 Cloudflare 页面上部署我的应用程序，但我认为 Remix 应用程序没有优化以减少工作人员请求的数量。

这源于 Remix 的内部工作方式。默认情况下，它会自动为您处理状态管理。每次调用表单操作时，都会使用新的服务器状态重新呈现 UI。由于加载器和动作函数在服务器上运行，持续的数据同步会增加您的成本，尤其是在无服务器的环境中。

我不知道对于像 Next.js 这样的其他选择是否也是如此，但是在为您的项目选择合适的框架时，这种默认行为可能是一个重要的考虑因素。

## 结论

React 使用起来很有趣。混音用起来很有趣。虽然我有一些担心，但是到目前为止，我很喜欢这个开发，我肯定会继续使用它。在接下来的几个月里，我会写更多关于我正在做的项目，也许我还会发现一些关于 Remix 的新的很酷的东西来分享:)

我希望你喜欢读这篇文章。如果你愿意支持我当作家，可以考虑报名 [*成为中等会员*](https://marplex.medium.com/membership) *。你可以以每周不到 1 美元的价格无限制地使用所有的媒体。*

[*作为一个媒介会员，你的会员费直接支持我和你阅读的其他作家。你也可以在媒体上看到所有的故事。*](https://marplex.medium.com/membership)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***