# 如何将 express-validator 与模式和自定义验证结合使用

> 原文：<https://javascript.plainenglish.io/how-to-use-express-validator-in-combination-with-schema-custom-validation-78bba466a246?source=collection_archive---------1----------------------->

## 关于如何在使用 ExpressJS 时进行服务器端验证的教程

![](img/c30ec58db5e3d5686b0ece4269b76adf.png)

Photo by [Brett Jordan](https://unsplash.com/es/@brett_jordan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/error?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 什么是 express-validator？

> express-validator 是一套 [express.js](http://expressjs.com/) 中间件，包装了 [validator.js](https://github.com/validatorjs/validator.js) 验证器和杀毒器功能。
> 
> 来源:[https://express-validator.github.io/docs/](https://express-validator.github.io/docs/)

如上所述，它是一个帮助验证数据的中间件。它已经存在了一段时间，也获得了对 TypeScript 的支持。

# 我们将实现什么？

在这篇文章中，我们将看到如何使用这个库进行服务器端验证。

因为这个包使用了[，](https://github.com/validatorjs/validator.js)你可以在这里得到可用验证器的列表-[https://github.com/validatorjs/validator.js](https://github.com/validatorjs/validator.js)

## 基本验证

我们将从一些基本的验证开始，如字段不能为空，或者必须是数字，或者是电子邮件等。这可以在路由级别上很容易地实现。例如，如果您有一个包含 3 个表单字段的 POST API route `/charity`，那么您可以像这样进行验证

basic validation using express-validator

这些验证器有许多组合，它们也可以被链接起来。请参考此处关于验证器[的文档。](https://github.com/validatorjs/validator.js)

## 基于模式的验证

上述设置的问题是，如果您有大量的字段要验证，那么您的路径将很快变得非常臃肿。为了帮助解决这种情况，express-validator 支持`Schema based validation`。

您可以基于您的数据模型定义一个模式，并传递它进行验证。

例如，如果您想要验证这样的数据模型

然后，像这样添加您的模式定义(我希望这些是一个新文件)

> 注意我们如何使用点符号来遍历数据。

现在，您所要做的就是像这样在您的路由定义中传递这个模式

这看起来更干净，更容易阅读，并且您可以在您可能需要的任何其他途径中共享相同的模式。

## 复杂情况下的中间件链

最后，如果您必须在这个基于模式的验证之上添加一些自定义验证，那么您也可以这样做。您可以将其作为中间件链接到您的路线中。

首先，像这样添加一个新的中间件功能-

注意，我们是如何通过添加错误消息来传递`error`数组的。它与上一步中模式验证函数填充的数组相同。

我们现在在路由定义中调用一个中间件，就像这样-

感谢您的阅读，如果您想支持我，请关注我，成为会员，让我们所有人都留在这个平台上。

[](https://medium.com/@metacollective/membership) [## 通过我的推荐链接加入媒体 Meta Collective

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@metacollective/membership) 

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*