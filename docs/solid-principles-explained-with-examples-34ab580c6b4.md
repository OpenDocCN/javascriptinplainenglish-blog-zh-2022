# 每个优秀的开发人员都应该知道的坚实的设计原则

> 原文：<https://javascript.plainenglish.io/solid-principles-explained-with-examples-34ab580c6b4?source=collection_archive---------10----------------------->

## 用实例解释坚实的设计原则

![](img/9a19dda956d2587f1ccf8e205bc16f0c.png)

Photo by [Ian Hutchinson](https://unsplash.com/@ianhutchinson92?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你使用面向对象编程或者熟悉它，坚实的原理是必须知道的。这五个软件开发原则是您在构建软件时可以遵循的指南，以使软件更易于维护和扩展。

这些原则更早就存在了，但是由于软件罗伯特·c·马丁(鲍勃大叔)在他 2000 年的论文 [*设计原则和设计模式*](https://web.archive.org/web/20150906155800/http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf) *中提到它们，这些原则变得流行起来。*

让我们开始吧。

## 单一责任原则

> 一个类应该有且只有一个责任

一个类应该有且只有一个责任
在下面的例子中，您可以看到`PasswordEncoder`类具有加密并将密码保存到数据库的功能。这个类违反了单一责任原则。

我们可以通过创建一个单独的类来处理将密码保存到数据库的功能，从而解决这个问题。这里我们确保每个类只有一个责任，而不是做多件事。

## 开/关原则

> 一个类应该对扩展开放，对修改关闭

您可以在下面的`PasswordEncoder`类中看到，它对不同类型的加密有不同的实现。如果我们想添加任何新的加密实现，我们需要修改它。这个类没有遵循开放/封闭原则，该原则规定一个类应该是可扩展的，但不应该根据新的需求进一步修改。

我们可以通过使用一个接口来解决这个问题，在这个接口中，我们指定了要做什么的抽象，这样它就可以根据需要进行扩展。根据需求，可以在不修改原始类的情况下添加新功能。

## 利斯科夫替代原理

> 派生类应该可以被它们的基类替换

在下面的`Encoder`类中，我们有一个`encode`方法，它获取一个密码，对其进行编码，然后将编码后的密码作为字符串返回。扩展它的子类几乎和基类做同样的事情，但是在`SHA256Encoder`类的情况下，它接受密码，但不返回加密的密码。这种行为违反了利斯科夫替代原理。

我们可以通过确保所有的实现都具有相同的行为并做与基类相同的事情来纠正这一点。因此，当我们需要用基类的实现替换子类的实现时，它不应该有不同的行为或返回与预期不同的结果。

在这个例子中，您可以看到，即使我们用基类的方法替换子类的方法，我们也可以确保它接受密码并返回该密码的加密形式。

## 界面分离原理

> *客户不应该被迫依赖他们不使用的方法。*

考虑下面的例子，其中`PasswordEncoder`类有编码和解码方法。这个类违反了接口隔离原则，因为不是所有的子类都想实现这两种方法。我们可以看到 SHA256 在技术上不能被解密，所以这个类没有实现 decode 方法。

我们可以通过拆分接口来解决这个问题，这样我们就不会有这种问题了，子类也不应该实现他们不需要的东西。通过这样做，子类将根据他们的需求实现他们需要的东西。

## 从属倒置原则

> 高层模块不应该依赖低层模块。两者都应该依赖于抽象。
> 
> 抽象不应该依赖于细节。细节应该依赖于抽象。

在下面的例子中，您可以看到`PasswordHelper`类违反了依赖反转原则，因为它被紧密绑定到 SHA256 编码器。

我们可以通过将其从使用 SHA256 编码器类中解耦来纠正这一点。

在这种情况下，最终用户可以决定他们想要使用哪种编码器实现的细节。所以我们不依赖于具体的底层实现，而是依赖于抽象。

这是五个坚实的原则，以及你需要遵循的东西，这样你的代码就容易维护、扩展和重用，而不必处理可能出现的问题。

我希望你已经发现它们有用。

感谢阅读！

## 参考

*   baeldung.com[上的坚实原则](https://www.baeldung.com/solid-principles)
*   坚实的原则在[freecodecamp.com](https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/)
*   面向对象的坚实原理在[DigitalOcean.com](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)

如果你喜欢阅读这样的故事，并想支持我成为一名作家，可以考虑[注册成为一名媒体会员](https://nehalk.medium.com/membership)。一个月 5 美元，你可以无限制地阅读 Medium 上的所有故事。如果你用我的链接注册，我会赚一点佣金。

[](https://nehalk.medium.com/membership) [## 通过我的推荐链接加入 Medium-Nehal Khan

### 阅读 Nehal Khan(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

nehalk.medium.com](https://nehalk.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*