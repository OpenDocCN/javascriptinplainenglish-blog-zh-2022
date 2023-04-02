# 关于如何将 Stripe API 与 JavaScript 一起使用的简短教程

> 原文：<https://javascript.plainenglish.io/a-short-introduction-to-using-stripe-api-with-javascript-9c83f89af1e1?source=collection_archive---------10----------------------->

![](img/555a19e062d60309e69bb76df7761a43.png)

Photo by [Blake Connally](https://unsplash.com/@blakeconnally)

## 以下是开始的方法。

Stripe 在许多年前开始作为一个面向开发者的不起眼的支付网关，但现在它正在展望未来，为未来的商业构建基础设施。如果您是一名对使用 JavaScript 开始使用 [Stripe API](https://stripe.com/docs/api) 感兴趣的开发人员，那么这篇文章就是为您准备的！

我将一步一步地讨论如何在 Stripe 测试帐户中创建测试产品，并使用 JavaScript 请求访问关于这些产品的信息。这将允许您在一个安全而又真实的环境中使用 API。

由于 Stripe API 功能强大，可以做很多事情，所以本文只讨论一个用例——即检索企业内部的产品信息。我将在这里介绍的是创建一个 Stripe 帐户，创建产品，将代码连接到您的帐户，以及获取关于您的产品的信息。

## 创建 Stripe 帐户—这是免费的！

你可以在这里创建一个免费的条纹账户[。一旦完成，您将可以访问在*测试模式*下激活的仪表板(您会看到一个被称为“测试模式”的开关被打开，可能在仪表板的右侧)。现在您已经有了这个测试帐户，您可以通过 Stripe API 来使用它。](https://stripe.com/)

接下来你要做的是为你的账户找到密钥。点击*开发者*标签，然后点击 *API 密匙*来查看你的公开密匙和秘密密匙。请保管好密钥，因为我们稍后将使用它通过您的代码连接到您的帐户！*注意:即使这是一个测试账户，也不要与他人分享你的密钥！*

## 创造产品

在您的仪表板中，单击*产品*选项卡将允许您添加新产品。对于本教程，我会添加一到四个产品。您可以给它们起产品名，如*测试产品 1* ，每个产品的价格为 *$0.00* 。如果需要，您可以随时编辑这些信息。

## 编写连接到您的帐户的代码

打开您喜欢的代码编辑器，创建一个新的 JavaScript 文件(例如，名为 *stripe_test.js* )。要运行这个文件，我建议安装 [Node.js](https://nodejs.org/en/) 。这样，您可以简单地在命令行中运行 node 来查看您的 JavaScript 程序的结果(例如， *node stripe_test.js* )。

现在是写代码的时候了。首先，通过在命令行中键入 *npm install stripe* 来安装您需要的依赖项(或者类似的 *yarn* )。然后，作为 JavaScript 的第一行，要求 Stripe 像这样:

`const Stripe = require(“stripe”);`

接下来，将您的密钥存储在一个变量中。关于这一点，请阅读下面的重要说明！

`const SECRET_KEY = ‘sk_test_51K8pTLKS5...........’;`

**重要提示** —通常，您会希望将任何密钥存储在一个*中。env* 文件，而不是将它们直接存储在代码中。然而，对于我们这里的目的，我们只是在您的本地机器上用一个测试帐户玩玩。如果您计划与他人共享您的代码，请使用*。env* 文件进行密钥存储，而不是像我上面所做的那样。为了了解更多关于在应用程序中存储密钥的信息，我在这里写了一篇文章。如果你在任何时候怀疑你的秘密密钥已经泄露给别人而不是你自己，你应该使用“滚动密钥”功能来改变你的密钥。

现在，选择一个你在你的账户中创建的随机产品，并获取它的 ID。你只需点击你账户中的一个产品就可以得到。你会在产品详情下看到它的 ID。将 ID 存储在您的代码中，就在您的密钥下面。当试图获得关于特定产品的信息时，这将很方便:

`const PRODUCT_ID = ‘prod_KoWtM......’;`

## 最后，获取产品信息

让我们编写一些请求来获取测试帐户中某个特定产品或几个产品的信息。

要获得关于存储在`PRODUCT_ID`中的特定产品的信息，您可以编写这样的请求，使用 *async await* 来检索数据:

```
const getSingleProduct = async (stripe) => {
    const product = await **stripe.products.retrieve(PRODUCT_ID)**;
    console.log(product);
}getSingleProduct(stripe);
```

当您运行您的程序时，您的控制台应该在产品 ID 下显示一个带有产品信息的对象，包括它的名称、相关图像等等！

既然您已经能够获得特定的产品，以下是您如何获得仪表板中列出的所有产品:

```
const getAllProducts = async (stripe) => {
    const product = await **stripe.products.list()**;
    console.log(product);
}getAllProducts(stripe);
```

哦，如果你只是想要几个产品(例如，只是你的三个产品)，你可以像下面这样做。如果您正在构建一个展示产品的网站，并希望引入分页或仅展示一些示例产品，这可能会有所帮助:

```
const getThreeProducts = async (stripe) => {
    const product = await **stripe.products.list({
        limit: 3
    })**;
    console.log(product);
}getThreeProducts(stripe);
```

这里的目标是介绍如何以简单易懂的方式将 Stripe API 与 JavaScript 结合使用。同样，Stripe API 可以做的事情比这里展示的要多得多，但我只是想触及皮毛。

我希望这个教程是有帮助的，感谢阅读！

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*