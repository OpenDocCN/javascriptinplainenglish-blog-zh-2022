# 为 Strapi V4 添加自定义用户权限提供程序

> 原文：<https://javascript.plainenglish.io/add-a-customize-users-permissions-provider-for-strapi-v4-6aa78c642977?source=collection_archive---------2----------------------->

## 关于如何为 Strapi V4 添加自定义用户权限提供程序的指南。

![](img/594225392bf810fe6a5a52a42dc77028.png)

Photo by [Desola Lanre-Ologun](https://unsplash.com/@desola?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**更新:**

根据[插件扩展——Strapi 开发者文档](https://docs.strapi.io/developer-docs/latest/development/plugins-extension.html#within-the-extensions-folder)，找到一个更简单的方法

在 src/extensions/users-permissions/strapi-server . js 中

```
'use strict';module.exports = (plugin) => {
 plugin.bootstrap = require('./server/bootstrap');
 plugin.services['providers'] = require('./server/services/providers');
 **return** plugin;
};
```

不需要。/src/extensions/users-permissions/server/index . js/src/extensions/users-permissions/server/service/index . js。

首先我们根据 Strapi V4 文档在我们的项目结构中的 src/extensions 文件夹下创建一个名为“users-permissions”的文件夹:[https://docs . Strapi . io/developer-docs/latest/development/plugins-extension . html # extending-a-plugin-s-interface](https://docs.strapi.io/developer-docs/latest/development/plugins-extension.html#extending-a-plugin-s-interface)。

因为 Users-Permissions provider 是一个“服务器”端插件代码，我们需要创建一个文件名为 strapi-server.js 的文件

然后我们需要创建相应的文件夹:

`./server/bootstrap and ./server/services.`

然后从 node _ modules/@ strapi/plugin-users-permissions/，复制一些源代码:

server/index.js、server/bootstrap/index.js、server/services/index.js 和 server/providers.js。

最后，我们有这样的文件和文件夹结构:

```
├──── src
│     ├──── [extensions](https://docs.strapi.io/developer-docs/latest/development/plugins-extension.html) # files to extend installed plugins
│     │     └──── users-permissions
│     │           ├──── server
│     │           │     └──── bootstrap
│     │           │     │     └ index.js 
│     │           │     └──── services
│     │           │     │     └ index.js
│     │           │     │     └ providers.js
│     │           │     └ index.js  
│     │           └ [strapi-server.js](https://docs.strapi.io/developer-docs/latest/developer-resources/plugin-api-reference/server.html)
```

在我们添加自定义提供程序代码之前，我们需要首先修复 requrie 文件路径。

在 server/index.js 中，将源代码修补为:

在 server/bootstrap/index.js 中，按如下方式修补源代码:

在 server/services/index.js 中，将源代码修补为:

现在是时候添加我们定制提供者源代码了！

在 server/bootstrap/index.js 中:

在 server/services/providers.js 中:

现在你知道了。感谢您的阅读。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/)***[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。****