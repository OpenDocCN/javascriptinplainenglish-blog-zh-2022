# 企业在 2022 年做出反应

> 原文：<https://javascript.plainenglish.io/enterprise-react-in-2022-3126ed43ba58?source=collection_archive---------0----------------------->

## 在 2022 年构建企业级 React 应用

![](img/b275227fe1e7f33b751774666c44c0ca.png)

学习 React 和能够用 React 开发企业级应用是两回事。这有两个主要原因。首先，有一个庞大的不同模块的生态系统需要你去掌握。第二，这个生态系统每年都在变化。我上一次展示 enterprise React 技术堆栈是在两年前的。正如您将看到的，该技术堆栈中没有多少模块能坚持到今年。因为在 React world 中导航可能会有挑战性，所以我写了这篇文章，它可以作为一张地图，帮助你了解令人兴奋的 React wonderland 的现状。

伴随本文而来的是 [GitHub repo](https://github.com/slava-lu/enterprise-react-2022) 和[演示应用](http://enterprise-react-2022.vercel.app)，它们集合了这里提到的所有模块(以及更多)。你可以把这个报告作为你下一个伟大的 React 应用的样板。

**TL；博士**

**主要模块**

[Next.js](https://nextjs.org/) — React SSR 框架

[Redux](https://redux.js.org/) —中央国家管理

[Next-redux-wrapper](https://github.com/kirill-konshin/next-redux-wrapper)—Next 和 Redux 连接器

[Redux-Saga](https://redux-saga.js.org/)—Redux 的异步中间件

[下一步-翻译](https://github.com/vinissimus/next-translate)-翻译和 i18n

[反应钩子表单](https://react-hook-form.com/) —表单库

[脉轮 UI](https://chakra-ui.com/) —设计系统

*演示*—[https://enterprise-react-2022 . vercel . app](https://enterprise-react-2022.vercel.app)

*回购*——[https://github.com/slava-lu/enterprise-react-2022](https://github.com/slava-lu/enterprise-react-2022)

从 2020 年开始的第一个大变化是服务器端渲染(SSR)现在是必须的。它不再仅仅是一种 SEO 技巧或性能优化方法。这是行业标准，无法避免。没有 SSR，在现代谷歌排名系统中获得任何好的分数几乎是不可能的。核心网站的生命力变得如此重要，以至于 SSR 主框架的学习门户网站已经将[的整个章节](https://nextjs.org/learn/seo/web-performance)专门用于这个主题。我建议把核心网站的重要功能掌握到一个很好的水平。随着信息量的不断增加，仅凭信息很难判断哪个网站更好。因此，检查开发人员为创建网站付出了多少努力可能会成为搜索引擎排名的关键因素。

构建基于 React 的 SSR 应用的关键框架是 **Next.js** 。目前没有真正的替代方案。Next.js 很容易上手，它有很好的入门指南和文档。你可以很容易地用它来构建一个简单的应用程序，但是对于企业级的应用程序来说就有点棘手了。问题是像 Redux 这样的中央状态管理，大多数大的 app 还是需要的。已经有很多尝试去摆脱 Redux 或者用别的东西来代替它，但是因为 Redux 提供了一个真正伟大的开发者体验，我确信它还会存在几年。

Redux 面临的挑战是它应该在客户端使用。每次在服务器上呈现一个页面，都会创建一个新的 Redux store，然后需要以某种方式将其与现有的客户端状态合并(这个过程称为水合)。水合作用可能很棘手，容易出错。最好的方法是将第一次呈现作为 SSR，创建一个新的干净的 Redux 存储，然后只进行客户端呈现。这正是 Next.js 引入 ***getInitialProps*** 数据获取方法的最初方法。出于某些原因，他们后来决定放弃这种方法，并引入了两种新方法，***getServerSideProps***和 ***getStaticProps*** 作为原始方法的潜在替代。Next.js 背后的公司 Vercel 声称，这两种新方法可以提高应用程序的性能。他们没有删除最初的 *getInitialProps* ，但是他们试图避免在他们的沟通和文档中提及它。getStaticProps 的目的是在构建期间呈现静态页面，然后只提供静态内容。我怀疑许多企业级应用程序有大量静态内容来大量使用这种方法。getStaticProps 的主要目标可能是竞争对手 Gatsby 和 T21 的框架。即使有 Vercel 的解释，getServerSideProps 的目的也不太清楚，并且对于 Next.js 是否真的应该推动开发人员社区使用这种方法还存在争议。不过很清楚的是 *getInitialProps* 与 Redux 一起工作得更好，完全杀死 *getInitialProps* 可以极大地减少 Next.js 的使用。由于如上所述 React world 中没有替代方案，这可能会激励开发人员尝试 [Vue.js](https://vuejs.org/) 和 [Nuxt.js](https://nuxtjs.org/) 并可能会继续使用。

现在还不清楚 Next.js 最终会向哪个方向发展。在演示应用程序中，我使用了所有三种数据获取方法来展示它们如何与 Redux 一起使用。正如你可能看到的 *getInitialProps* 提供了比其他两种方法更流畅的开发体验。

对于处理 REST API(以及 WebSocket)的 Redux 中间件，我建议使用好的老式 **Redux-Saga** 模块。它很好地分离了 UI 和业务逻辑，使得管理复杂的业务逻辑变得非常简单。公平地说，最初学习 Redux-Saga 可能会很耗时，但之后你将会以光速构建你的异步中间件。

如果您关注 React 趋势，您可能会注意到有人建议将数据获取逻辑移到组件级别，但我猜想这可能只是最终杀死 Redux 的又一次尝试。我看不出它对大型应用程序有什么真正的好处。UI 与数据提取逻辑的分离提高了应用的可靠性，改善了开发人员的体验。如今，开发者体验变得越来越重要。技术变得复杂，学习变得困难，人类很难理解，更不用说掌握所有新兴技术。因此，让事情变得简单可能是选择一种技术而不是另一种技术的决定性因素。

当与 Next.js 一起使用时，Redux-Saga 的一个额外好处是，您可以轻松地选择您的数据获取/导航策略。有两种主要方法:

1.  首先导航到一个新页面，然后获取数据。
2.  首先获取数据，然后导航。

第一种方法看起来更受欢迎，但是用 Next.js 作为数据获取方法并不容易实现，不管它们是什么，都会阻碍页面导航。Redux-Saga 允许您选择是否要在导航之前等待数据呼叫完成(承诺已解决),因此，可以轻松实现任何选项。如何做到这一点可以在演示应用程序中看到。在源代码中寻找 *navigateAfterSaga* prop。

```
*Shop*.getInitialProps = async ({ store }) => {
  store.dispatch(*triggerProductList*(10))
  return {
    **navigateAfterSaga**: false,
    title: 'title#shop_page',
  }
}
```

至于底层数据取数函数，这次我用 [**Axios**](https://axios-http.com/) 代替了经典取数。这主要是因为 Axios 在客户端和服务器上都很好地管理了超时功能。老实说，我甚至不知道如何用 fetch 和 Next.js 管理服务器上的超时。

Next.js 的一个很好的新特性是开箱即用的国际化路由。不幸的是，它只是开发人员构建多语言应用程序所需的一小部分。你至少还需要一个翻译模块。您应该仔细选择一个，因为不是所有的翻译模块都支持所有的 Next.js 数据获取方法。我推荐使用 **next-translate** ，因为它支持 *getInitialProps* 。

另一个好的多语言应用可能需要的特性是根据语言改变 URL 路径。不仅是语言前缀，还有整个路径，例如' *en/page'* 变成' *de/seite '。*这据称是通过 Next.js [重写](https://nextjs.org/docs/api-reference/next.config.js/rewrites)特性实现的。但绝对不是它应该属于的地方。我希望 Next.js 能在未来的某个时候解决这个问题。

在技术堆栈选择过程中，您需要做出的一个重要选择是 UI 库。你可以自己做，但是你需要很大的努力。有一些现成的解决方案，今天 React 世界的明显领导者是 **Chakra UI** 。以前材料用户界面是首选，但是人们已经厌倦了它，这种设计系统的发展也不是很活跃。Chakra 提供了一系列[基本免费元素](https://chakra-ui.com/docs/getting-started)以及付费[专业版](https://pro.chakra-ui.com/)中的预建模板。使用 Pro templates，你可以在几天内创建你的电子商务 web 应用程序的 UI，而不需要 Figma 或任何其他设计工具。这真的很酷。

和其他 UI 库一样，问题是它强迫你使用自己的 API。如果你已经学会了所有的 CSS 属性，你必须用 Chakra UI 重新学习。这有点烦人，但是你可以把最常用的列表打印出来，夹在你面前的某个地方。对于非常复杂或独特的 UI 元素，我建议使用[样式组件](https://styled-components.com/)库，因为它提供了很大的灵活性，并且使用标准 CSS。没有缩写或驼色替代品。

在表单管理方面，React 生态系统有一个新的年轻领导者。在最初的 [Redux Form](https://redux-form.com/) 之后，短时间内流行的选项是 [Formik](https://formik.org/) 。Formik 的问题是它使用了渲染道具模式。这种模式曾经被认为是流行的，因此被许多模块使用。这种模式虽然没有持续很长时间。我发现这种模式令人困惑，对于复杂的应用程序，很难看出代码中发生了什么。

为了解决 Formik 和以前的表单库的问题，新的播放器出现了，现在正在积极地获得动力——反应钩子表单。它易于使用和理解。主要的挑战来自于它是基于不受控制的表单模式。因此，在表单组件之外提交表单变得很复杂，但也不是不可能。简单性和良好的文档是这个库的杀手锏。

这是您可以用来开始构建专业企业级 React 应用程序的主要模块的概述。

简单说说**的部署**。如果你用 Next.js 开发了这个应用，你应该考虑把它部署到 [Vercel hosting](https://vercel.com/) 。你只需将 GitHub repo 连接到 Vercel cloud，点击几个按钮就可以发布了。更有用的是，您可以从包装盒中取出 CI/CD。一旦创建了拉请求，您就可以获得预览部署，并且一旦将拉请求合并到主/主要分支，您的生产部署就会更新。如果你曾经试图在 Jenkins 或 GitHub Actions 中配置这种功能，你会喜欢这个特性的。

还有几个其他重要的主题与 React 没有直接关系，而是总体上与前端领域有关，所以我将简要地介绍一下。

**测试**。测试比看起来要复杂。一方面，每个人都声称测试是重要的，但是少数人可以更深入地探究测试是重要的以及为什么重要。大多数单元测试宣传来自后端世界，在那里，当开发人员编写代码时，没有即时的反馈。对于后端开发人员来说，在代码进入生产系统之前，查看它们是否真正工作的唯一简单方法是用单元测试来测试它。但在现代前端世界，情况并非如此。利用 Next.js 和其他框架提供的当前高性能和可靠的[快速刷新](https://nextjs.org/docs/basic-features/fast-refresh)特性，前端开发人员可以立即看到他们键入的每一行代码的结果。将这一点与基于组件的方法相结合，这种方法将代码从相互影响中分离出来(特别是如果您使用 Redux Saga 将 UI 从数据层中分离出来)，单元测试的价值变得不那么明显。我敢大胆地说，单元测试对 React 应用程序没有什么价值，除非你有一些复杂数据操作的文件。但是如果你这样做，我强烈建议检查这段代码是否属于后端。

前端测试中真正有用的是端到端的 UI 测试。前端开发人员通常很难看出图片的边框半径是 4 px 而不是 2px，或者元素之间的间距增加了 4px。这种类型的 UI 测试可以用许多好的工具来自动化。另外，用一些自动化工具随机点击链接和按钮也会有所帮助。开发人员通常会检查理性人会选择的逻辑路径。随意点击按钮可能会使网站关闭或导致不一致的状态。最好避免这种情况。

我想谈的最后一个话题是第三方服务。如今，没有人想去摆弄邮件服务器和其他与基础设施相关的软件。为了节省你搜索可用选项的时间，我在下面列出了我的个人偏好。为了保持这篇文章相对简短，我不会给出任何论据，但如果你想谈论它，请随意使用评论。

[Cloudinary](https://cloudinary.com/) —存储和提供所有媒体文件

[发送网格](https://sendgrid.com/) —发送技术邮件

[Mailchimp](https://mailchimp.com/)——发送营销邮件

[Sendbird](https://sendbird.com/) —聊天和其他消息功能

许多人可能会争辩说，他们设法使用一套不同的模块来构建伟大的应用程序。很可能这是真的。但是我可以向你保证的是，如果你选择了这里介绍的技术，你不会后悔你的选择。

我希望这个概述对您有所帮助。请随时关注我，了解 React 的最新趋势，或者如果您有什么要补充或不同意的，请发表评论。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***