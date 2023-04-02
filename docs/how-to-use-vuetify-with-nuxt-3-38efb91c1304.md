# 如何在 Nuxt 3 中使用 Vuetify

> 原文：<https://javascript.plainenglish.io/how-to-use-vuetify-with-nuxt-3-38efb91c1304?source=collection_archive---------7----------------------->

## *结合使用最新版本的 Vuetify 和 Nuxt。*

![](img/f1c77f9d18a9a6637fb86e690a29e8c8.png)

# 装置

如果您还没有一个 Nuxt 3 项目，那么从创建它开始。

```
npx nuxi init nuxt-app
```

然后运行`cd nuxt-app`和`yarn`来确保您的依赖项已经安装。

现在我们的 Nuxt 3 项目已经建立，我们准备集成 Vuetify。当您在 Nuxt 应用程序的根目录中时，运行以下命令来安装 Vuetify 3 及其依赖项 sass。

```
yarn add vuetify@next sass
```

您的`package.json`现在看起来应该如下所示:

```
// package.json"devDependencies": { "nuxt": "3.0.0-rc.1"},"dependencies": { "sass": "^1.51.0", "vuetify": "^3.0.0-beta.1"}
```

# 创建我们的 Vuetify 插件

我们已经安装了 Vuetify，现在我们需要它来与 Nuxt 对话。我们将通过使用 Nuxt 的[插件(打开新窗口)](https://v3.nuxtjs.org/guide/directory-structure/plugins/)特性来实现。

创建一个`plugins`文件夹，然后创建一个名为`vuetify.js`的文件，并把它放在新创建的插件文件夹中。

然后，在`vuetify.js`文件中，粘贴以下代码:

```
// plugins/vuetify.jsimport { createVuetify } from 'vuetify'import * as components from 'vuetify/components'import * as directives from 'vuetify/directives'export default defineNuxtPlugin(nuxtApp => { const vuetify = createVuetify({ components, directives,})nuxtApp.vueApp.use(vuetify)})
```

这主要记录在 Vuetify 的解释中。关键的区别是我们使用了`nuxtApp.vueApp.use(vuetify)`而不是`app.use(vuetify)`。

# 配置 Nuxt 3 使用我们的新插件

我们的最后一点配置出现在我们的`nuxt.config.ts`文件中。这是我们告诉 Nuxt 如何正确地找到和构建 Vuetify 的 sass 的地方。

```
// nuxt.config.tsimport { defineNuxtConfig } from 'nuxt'// https://v3.nuxtjs.org/api/configuration/nuxt.configexport default defineNuxtConfig({ css: ['vuetify/lib/styles/main.sass'], build: { transpile: ['vuetify'], },vite: { define: { 'process.env.DEBUG': false, }, },})
```

# 与 Nuxt 3 一起享受 Vuetify

现在一切都应该正常工作了，您应该能够在您的 Nuxt 页面中使用广泛的 Vuetify 组件了！

尽情享受吧！

*原载于*[*https://codybontecou.com*](https://codybontecou.com/how-to-use-vuetify-with-nuxt-3.html)*。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*