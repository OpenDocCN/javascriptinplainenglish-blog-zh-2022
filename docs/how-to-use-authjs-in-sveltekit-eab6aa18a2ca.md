# 简化 SvelteKit 中的身份验证

> 原文：<https://javascript.plainenglish.io/how-to-use-authjs-in-sveltekit-eab6aa18a2ca?source=collection_archive---------1----------------------->

## 如何将 SvelteKit 与 AuthJS 一起使用

![](img/1bd783232d998ff5e6e7b846fe15f832.png)

Photo by [Franck](https://unsplash.com/es/@franckinjapan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

NextAuth 的团队一直在努力从 NextAuth 中剥离认证逻辑，并创建新的 AuthJS 核心库。AuthJS 核心是框架不可知的，该团队已经发布了第一个适配器，目标是 SvelteKit。下面我们就来看看如何在实践中使用。

# **设置**

创建一个新的 SvelteKit 项目，选择骨架模板并使用 TypeScript:

```
npm init svelte@next svelteauth-demo
cd svelteauth-demo
```

为 AuthJS 安装 SvelteKit 适配器和核心:

```
npm install @auth/core @auth/sveltekit
```

# **认证提供者**

接下来，我们需要配置我们想要使用的身份验证提供者。对于这个演示，我们将使用 GitHub。在`src`目录中创建一个名为`hooks.server.ts`的新文件，并添加以下代码:

```
import { SvelteKitAuth } from "@auth/sveltekit"
import GitHub from '@auth/core/providers/github';
import { GITHUB_ID, GITHUB_SECRET } from "$env/static/private"

export const handle = SvelteKitAuth({
  providers: [
    GitHub({
      clientId: GITHUB_ID,
      clientSecret: GITHUB_SECRET
    })
  ]
});
```

导出的`[handle](https://kit.svelte.dev/docs/hooks#server-hooks-handle)`函数能够拦截对服务器的请求并处理认证。`clientId`和`clientSecret`作为环境变量传入。我们接下来将设置这些。

# **GitHub OAuth**

去 [GitHub 的开发者设置](https://github.com/settings/developers)创建一个新的 OAuth 应用。将回拨 URL 设置为`http://localhost:5173/auth/callback/github`。`http://localhost:5173`部分是 SvelteKit 的默认 URL。如果您正在使用不同的端口，或者正在部署您的应用程序，您需要对此进行更改。您还需要将“主页 URL”设置为`http://localhost:5173`。为下一步保存客户端 ID 和客户端密码。

# **配置环境变量**

接下来，我们需要配置环境变量。在项目的根目录下创建一个名为`.env`的新文件，并添加以下内容，用您自己的值替换占位符。`AUTH_SECRET`必须是 32 个字符的随机字符串。文档建议在 Linux 上使用`openssl rand -hex 32`生成一个，或者可以导航到[generate-secret . vercel . app](https://generate-secret.vercel.app/32)在浏览器中生成一个。

```
GITHUB_ID=<your-github-id>
GITHUB_SECRET=<your-github-secret>
AUTH_SECRET=<auth-secret>
```

# **获取会话**

现在我们需要获取会话数据。在`src/routes`目录中创建一个名为`+page.server.ts`的新文件，并导出一个返回会话数据的`load`函数:

```
import type { PageServerLoad } from "./$types"

export const load: PageServerLoad = async (event) => {
  return {
    session: await event.locals.getSession(),
  }
}
```

# **添加登录动作**

现在，我们需要向应用程序添加一些操作。导航到`src/routes/+page.svelte`并添加以下代码:

```
<script>
 import { signIn, signOut } from '@auth/sveltekit/client';
 import { page } from '$app/stores';
</script>

<p>
 {#if Object.keys($page.data.session || {}).length}

    {#if $page.data.session?.user?.image}
      <img
        src={$page.data.session?.user?.image}
        alt={$page.data.session?.user?.name}
        style="width: 64px; height: 64px;" />
      <br/>
  {/if}
  <span>
   <strong>{$page.data.session?.user?.email || $page.data.session?.user?.name}</strong>
  </span>
    <br/>
    <span>Session expires: {new Date($page.data.session?.expires ?? 0).toUTCString()}</span>
    <br/>
  <button on:click={() => signOut()} class="button">Sign out</button>

  {:else}
  <span>You are not signed in</span><br/>
  <button on:click={() => signIn('github')}>Sign In with GitHub</button>
 {/if}
</p>
```

使用`npm run dev`运行应用程序，导航到`http://localhost:5173`并试用它！

# **结论**

AuthJS 是一个了不起的库，它简化了许多不同帐户提供商的身份验证。从 GitHub 到 Twitter，甚至只是普通的旧电子邮件和密码，或者神奇的链接，AuthJS 都能帮你搞定。我已经开始迁移我自己的项目来使用这个库，因为它很容易使用，甚至可以处理会话数据。我希望你喜欢这个教程，我也希望你能给 AuthJS 一个尝试！

请注意，AuthJS SvelteKit 集成仍在开发中，文档还没有完成，但是经过一点尝试和错误，以及现有的 NextAuth 文档，不需要很长时间就可以找出任何缺失的部分。一定要给团队一些爱，在 [GitHub](https://github.com/nextauthjs/next-auth) 上启动项目。

[](https://differ.plainenglish.io/p/stylify-css-code-your-sveltekit-website-faster-with-csslike-utilities-ly2ujg9f) [## 风格化 CSS:用类似 CSS 的工具更快地编写你的 SvelteKit 网站

### Stylify + SvelteKit。使用 Stylify 更快地设计您的 SvelteKit 网站。不要研究选择器和语法。使用纯 CSS…

different . plain English . io](https://differ.plainenglish.io/p/stylify-css-code-your-sveltekit-website-faster-with-csslike-utilities-ly2ujg9f) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*