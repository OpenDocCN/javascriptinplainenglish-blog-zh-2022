# 用每个人都喜欢的 Svelkit 和 Django Rest 框架创建一个成熟的 Web 应用程序

> 原文：<https://javascript.plainenglish.io/creating-a-full-fledged-web-app-with-everyones-favorite-svelkit-and-django-rest-framework-79c5b72b9293?source=collection_archive---------2----------------------->

## 嘿，德夫斯！是的，我使用 SvelteKit 进行生产。

我是一名 Django 开发者，在网上学习了很多新东西，而 Svelte 是相当新的。我最近将我的基于 Django 的 web 应用程序迁移到了 SvelteKit，使用的是基于 Django Rest 框架的 web 应用程序。

在发展的过程中，老实说，我少挣扎了，你知道为什么吗？因为 Svelte 的简单……以及它提供的开箱即用的功能实在是太酷了。

今天，我将向你展示 Svelte 拥有的一些好的特性，我如何将 **Django Rest 框架与 SvelteKit** 一起使用，为什么 SvelteKit 对我来说是“最好的”前端/全栈 JS 框架，以及为什么我将在我的新独立项目中使用它？

我从它(苗条身材)的酷的内置功能和它的特色开始

*   过渡和动画效果，根据条件，只需一行代码
*   使添加扩展、包和库变得容易；比如顺风 CSS。
*   Svelte 极其简单，非常在意“DX”[开发者体验]
*   Svelte 以非常小的构建尺寸进行渲染的速度非常快
*   Svelte 提供内置适配器或自定义适配器，您可以使用它们来部署您的 web 应用程序
*   有了所有的特性，你就真正拥有了代码，你不会失去控制
*   HTML、CSS 和 JS 部分在同一个`.svelte`文件中协同工作，这使得编写代码更加容易，可读性也得到了增强。

这样的例子不胜枚举。所以，这些是我认为苗条很棒的一些基本原因。

不仅如此，SvelteKit 提供了额外的功能，使您的开发过程顺利进行；包括前端和后端。

Svelte 和 SvelteKit 有什么区别？ [**Kit 不是建立在 Svelte**](https://joyofcode.xyz/learn-how-sveltekit-works) **之上，而是一个后端 web 框架，Svelte 被用作视图层，或者说是组件处理程序。**

现在，正如我已经提到的，我要谈谈“我是如何将 DRF [Django Rest 框架]与 SvelteKit 结合使用的？”

## 我如何使用 DRF [Django Rest 框架]与 SvelteKit？

在我谈论上面的话题之前，我想和你谈谈，“为什么我用 SvelteKit 做网站开发？”嗯，说实话，感觉很酷。为了解释清楚，以下是我使用 SvelteKit 的一些原因…

*   SvelteKit 提供了`[form-actions](https://kit.svelte.dev/docs/form-actions)`,我可以用它轻松安全地提交安全的、基于授权的表单。
*   SvelteKit 与 Tailwind CSS 配合得很好，因为它有一个用于这项任务的`svelte-add`。即使 Tailwind CSS IntelliSense 无法与超级最新版本配合使用。
*   Svelte 提供了漂亮的内置过渡、效果和动画，我可以很容易地在我的 SvelteKit 项目中使用它们。
*   SvelteKit 有在每个 HTTP 调用中执行的`hooks.server.ts`,在这里我们可以编写我们的认证逻辑/算法。而`hooks.server.ts`可以在所有组件上返回值，可以超级轻松地抓取。
*   SvelteKit 有`+page.server.ts`和`+page.ts`，我可以在那里写一些`load`函数和“表单动作”。在页面加载到浏览器之前，`load`函数在服务器中执行。它主要用于向基于 SSR(服务器端呈现)的页面发送数据。
*   **苗条**有简单的上下文/商店处理，【`[writables](https://svelte.dev/tutorial/writable-stores)`苗条】

所以是的，这就是为什么我用了 SvelteKit。

所以，最初，我已经有了一个生产运行的 Django 项目，使用 PostgreSQL 作为它的数据库。我有代码，我调整它使它与 Django Rest 框架兼容。

我必须添加一些序列化器，并为新特性在模型中添加一些新字段。我这样做了，并用 PostMan 和 DRF 提供的`APITestCase`类进行了测试。

现在，轮到认证了。对于认证，我使用了一个名为`[Django Simple JWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/)`的库，它工作得相当好。`TokenObtainPairView`、`TokenRefreshView`、`TokenVerifyView`分别用于 URL`login/`、`refresh/`和`verify/`。

我使用`+page.server.ts`向 Django 后端请求，并将响应返回给 SvelteKit 的前端。基本上，SvelteKit 就像后端一样存储 cookies 和 JWT 令牌，中间端到达实际的 API 并将响应返回给前端。

我会做一篇“如何用 Django 认证/授权 SvelteKit”的描述性文章。

完成开发后，是时候从基于 Django 的系统迁移/部署到基于 SvelteKit / Django Rest 框架的系统了。

当我正在配置迁移时，AWS Lightsail 服务器突然卡住了，我不得不重启服务器系统。服务器重启后，失去了 PostgreSQL 的 DB 集群。我试着恢复了两天…没有成功。我失去了 3000+用户的数据库，存储了 7400+网址。

您可能会想到备份/快照，我将制作一个新的故事“我是如何失去 3000 多个用户的数据库的？”

最后，我刚刚创建了一个新的 PostgreSQL DB 实例，带有一个新表。并将其与 DRF 后端连接起来。我用 pm2 和`@sveltejs/adapter-node`部署了 SvelteKit 应用程序，进行得相当顺利。

Django 后端使用了`nginx`和`gunicorn`来托管它。

所以，这是最终产品，它被称为 [Xoomato 网址卫士](https://xoomato.com/)。它通常是为想要在社交媒体上安全地分享他们的网站的 Adsense 发布者准备的。

未完待续…

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*