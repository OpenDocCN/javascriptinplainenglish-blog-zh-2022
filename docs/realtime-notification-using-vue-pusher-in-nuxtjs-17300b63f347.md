# 使用 Nuxt.js 中的 Vue Pusher 进行实时通知

> 原文：<https://javascript.plainenglish.io/realtime-notification-using-vue-pusher-in-nuxtjs-17300b63f347?source=collection_archive---------5----------------------->

![](img/6d47e2e0d5f5cde9485818a523974707.png)

我想在我的 web 应用程序上获得实时通知。我尝试了不同的软件包，最终通过使用 Vue pusher 使它工作。所以，我会试着解释一下 Nuxt.js 中 Vue pusher 的实现。

首先，

```
npm i vue-pusher
```

然后，创建一个插件 pusher.js:

```
import Vue from 'vue';import * as Cookies from 'js-cookie'const token = Cookies.get('');Vue.use(require('vue-pusher'), {api_key: '9a104d47d5d64f496aaacccass',options: {cluster: 'ap2',forceTLS: true,encrypted: true,authEndpoint: process.env.BASE_URL+'/broadcasting/auth',auth: {headers: {'Authorization': `Bearer ${token}`,}},}});
```

将创建的插件添加到 nuxt.config.js 中:

```
plugins: [{src: '~/plugins/pusher', ssr: false},],
```

最后，在任何组件中使用 Vue 推动器，如下所示。

```
getProductStatusNotification() {var channel = this.$pusher.subscribe("private-product.status.changed");channel.bind("product-status-changed", (log) => {let notifications = log;});},
```

对于专用频道，请在频道名称前添加 private，对于公共频道，通常只使用频道名称。然后使用 channel.bind 使用事件通道名称，通道事件由后端提供。

点击查看推手官方文件[。](https://pusher.com/tutorials/realtime-app-vuejs/)

此外，还要检查一下[推杆](https://www.npmjs.com/package/vue-pusher)包。

给我买杯咖啡【https://www.buymeacoffee.com/ewumesh 

在 Instagram 上关注我:[https://www.instagram.com/ewumesh](https://www.instagram.com/ewumesh/)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***