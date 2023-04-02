# 带反应和条纹的购物车

> 原文：<https://javascript.plainenglish.io/shopping-cart-with-react-and-stripe-fbbd6ec8d448?source=collection_archive---------3----------------------->

## 现实世界电子商务项目的优秀教程

![](img/0df128ff317ec1e11bb60310368dc671.png)

Photo by [Blake Wisz](https://unsplash.com/@blakewisz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

做一个电商网站最重要的部分就是如何连接前端和后端。**库珀代码教程**刷新了我对这个话题的看法。

链接到他的[教程](https://www.youtube.com/watch?v=_8M-YVY76O8&t=61s&ab_channel=TraversyMedia)

GitHub [代码](https://github.com/coopercodes/ReactEcommerceStoreWithStripeAPI)

第一部分是构建购物页面的**前端**。

文件夹结构:

![](img/637f7f93e064a25fbe1dadbc4d5d31a1.png)

要安装哪些依赖项:

![](img/a79bb44b1ad226fb81d040ada8db5bb4.png)

对于前端， *react-bootstrap* 用于样式化，而 *react-router-dom* 用于路由页面。

对于后端来说， *express js* 是针对 node js web 应用框架， *cors* 是针对 express 的中间件(或者有个替代品叫 body-parser)，而 *Stripe* 是在线支付 API。

从 **App.js** 可以看出，整个项目包括三个页面，主*商店页面*，支付成功时的*成功页面*，取消支付时的*取消页面*。

![](img/4ba3a84cc8c0fb453584294bef3dcc42.png)

Navbar 包括使用 React-bootstrap 的 Navbar。

![](img/1a5c413388416090fe0ed84015e4c547.png)![](img/b45b10024fdffd28e003970cb5616fb9.png)

点击按钮时，显示*显示*

![](img/c36d902a2f937fe778ad64bc4fdb4bc7.png)

在导航栏之后， **Modal** 是显示购物车商品的框。

![](img/8e818154e40aaff4c21a3cb85d34ffed.png)

显示购物车中的所有商品。

所有产品数据都在 *productsStore.js.* 中

![](img/f1f3c67861acb32d9b8d659e2e7bdb27.png)

产品列表是一个用 Stripe 连接的 id 为的数组(后面我会解释)。 *getProductData* 按 id 为所有上下文使用。

所有购物车逻辑代码都在 *cartContext.js* 中

![](img/fdb0d48e88a8f808a0ec87cfb283c1a9.png)

用`createContext()` 创建 cartContext，并用 Provider 传递值。

购物车有**四个功能:添加商品、移除商品、删除商品和获取总价。**

![](img/80ea6bb712ccd299747e7abc9e5abb7f.png)

addOneToCart

如果数量为 0，则在 cartProducts 数组中添加新项目，或者将数量加 1。和从购物车中减少一个是一样的。

![](img/5ecdb372b670dc9b7df049d691e3eefa.png)

removeOneFromCart

然后从购物车中删除商品:

![](img/f0ea2a5ad528fee375a97c73e8631e8b.png)

deleteFromCart

过滤不同 id 的 cartProduct

![](img/a470cc2cbf6c21d61de89081479e9282.png)

getTotalCost

用`reduce()`按单价和数量计算总价

![](img/1b90ecfeaec6b243a73903675c7c4ca9.png)

商店页面包括产品卡:

![](img/adecb025fcbdfd43116e5976d8c98ee7.png)![](img/9ef37f090906af9d58deef90a8ed39f2.png)

productCard

每张卡片都包含标题、价格和控制数量的按钮。当没有产品时，按钮显示添加到购物车，或者用`…?..:..`从购物车中删除

**后端，server.js.**

首先，注册[条带](https://stripe.com/)以获得秘密 API 密钥。并添加每个产品以获得下面的密钥

![](img/2fb8f8efcc02bf4143abdc34fa5bfb6f.png)![](img/de4bc39afeb5656839286233b0decebc.png)![](img/f3842f355ae16818e47403febbd8010a.png)

当您获得 API ID 时，按照我之前所说的，在 products 数组 ID 中替换它。

![](img/c0fc1b116b0ab5f4e86dd42b4c2c5d36.png)

并且记得设置账户处理支付功能。

![](img/8c8f0ed927ea91d3c7a972a897d7f2b1.png)

用`app.use()`运行每个库

并在结账时发布获取购物车中的商品，如果支付成功，重定向到成功 URL，要么取消 URL。并将响应发送回用户。

![](img/0ce674fd26e3f8e13809f21fb2c45a98.png)

并在端口 4000 上监听它。

![](img/271a77af5f5503650d2c6e84d7fd9cbe.png)

更多的[条带文档](https://stripe.com/docs/checkout/quickstart?client=react&lang=node)用于创建结帐会话。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*