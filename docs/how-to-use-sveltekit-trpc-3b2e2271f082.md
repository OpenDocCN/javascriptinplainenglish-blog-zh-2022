# 如何使用 SvelteKit + tRPC

> 原文：<https://javascript.plainenglish.io/how-to-use-sveltekit-trpc-3b2e2271f082?source=collection_archive---------4----------------------->

![](img/35f4619aaea6019c2a74eec18b2a197b.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

tRPC 是一个不可思议的库，它带来了类型安全的客户机/服务器函数调用，而没有代码生成的膨胀。虽然它没有 SvelteKit 的官方插件，但它很容易添加，今天我们将向您展示如何添加。

# **设置**

要跟进，导航到您现有的 SvelteKit 项目，或者按照下面的说明创建一个新的项目。确保在您的项目中启用了 TypeScript，否则您将错过 tRPC 最重要的好处！

```
npm create svelte@latest my-app # be sure to select `Yes, using TypeScript syntax`
cd my-app
npm i
```

# **安装 tRPC 和 Zod？**

tRPC 本身并不在运行时对输入进行类型检查，而是允许您自带验证器。Zod 是推荐的包，也是我们今天要用的包，但是它也支持像 Yup 和 SuperStruct 这样的东西。Zod 将允许我们定义一个模式，然后 tRPC 继承它进行输入。然后，Zod 将在运行时进行类型检查，如果请求不符合模式，就会相应地失败。

```
npm i @trpc/server @trpc/client zod
```

# **定义路由器**

路由器保存了我们所有的程序。过程只是一个输入模式和一个返回响应的方法。这映射到一个 API 端点。我们将在`src/lib/trpc/server.ts`中创建它。

为了定义我们的路由器，我们首先初始化 tRPC。return 名称空间用于定义我们所有的路由器和过程需求。调用`t.router`创建一个路由器，作为唯一的参数，我们有一个对象，将名称映射到过程。我们将创建一个简单的`hello`查询过程，它接受单个字符串作为输入。然后我们将返回前缀为`Hello` 的字符串。最后，我们将路由器的类型与路由器分开导出，以备后用。

```
import { initTRPC } from '@trpc/server';
import { z } from 'zod';

const t = initTRPC.create();

export const appRouter = t.router({
 hello: t.procedure.input(z.string()).query(async (opt) => {
    return `Hello ${opt.input}`;
 }),
});

export type AppRouter = typeof appRouter;
```

# **使用钩子接受请求**

现在我们有了一个路由器，我们需要将请求路由到该路由器，并返回响应。SvelteKit 给了我们`handle`钩子来做这件事。在`src/hooks.server.ts`中创建钩子。handle 钩子拦截所有对服务器的请求，在我们的例子中，可以完全覆盖某个 API 路由的行为(`/api/trpc`)。当我们检测到对该路由的请求时，我们使用 tRPC 的处理程序进行获取，并将响应返回给客户端。

```
import type { Handle } from '@sveltejs/kit';
import { fetchRequestHandler } from '@trpc/server/adapters/fetch';
import { appRouter } from '$lib/trpc/server';

const trpcPathBase = '/api/trpc';

export const handle: Handle = async ({ event, resolve }) => {
 if (event.url.pathname.startsWith(`${trpcPathBase}/`)) {
  const response = await fetchRequestHandler({
   endpoint: trpcPathBase,
   req: event.request,
   router: appRouter,
   createContext() {
    return {
     req: event.request,
    };
   },
  });

  return response;
 }

 return await resolve(event);
};
```

# **使用客户端创建&**

我们现在可以提出请求，但首先需要一个客户端。在`src/lib/trpc/client.ts`中，创建一个代理客户机并传递 url 选项，这样客户机就知道向哪里发送请求。我们将使用 localhost 进行开发，使用我们的部署域进行生产。

```
import { createTRPCProxyClient, httpBatchLink } from '@trpc/client';
import type { AppRouter } from './server';
import { dev } from '$app/environment';

export const trpc = createTRPCProxyClient<AppRouter>({
 links: [
  httpBatchLink({
      // url is dependent on the environment
      // in dev, we use localhost
      // in prod, we use the public domain
   url: dev
    ? 'http://localhost:5173/api/trpc'
    : `https://example.com/api/trpc`,
  }),
 ],
});
```

现在，在`src/routes/+page.svelte`中导入客户端，并观察神奇的类型推断在起作用。

```
<script lang="ts">
  import { trpc } from '$lib/trpc/client'

  async function hello(s: string) {
    return await trpc.hello.query(s);
  }
</script>
```

# **结论**

tRPC 给 fullstack TypeScript 项目带来了如此多的价值。在服务器上编写一次方法，然后从客户端调用该方法而不需要代码生成步骤的能力令人难以置信。虽然有一些警告，比如要求前端和后端都在同一个 repo (monorepos)中，并且只支持 TypeScript，但这是大多数项目所需要的。

# **资源**

-完成 [SvelteKit + tRPC](https://github.com/TheOtterlord/sveltekit-trpc) 模板
- [tRPC 文档](https://trpc.io/docs/)
-[Zod](https://zod.dev/)
-[SvelteKit 挂钩](https://kit.svelte.dev/docs/hooks)

*更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，*** *和*[*****不和* 【T63** *对成长黑客感兴趣？检查出***](https://discord.gg/GtDtUAvyhW) **[***电路***](https://circuit.ooo/) ***。*******