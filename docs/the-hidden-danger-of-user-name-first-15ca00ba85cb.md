# 用户的隐患？。名字？。第一

> 原文：<https://javascript.plainenglish.io/the-hidden-danger-of-user-name-first-15ca00ba85cb?source=collection_archive---------4----------------------->

![](img/68240be73752f6dcb2d88bb17ae655d0.png)

Photo by [Kyle Sudu](https://unsplash.com/@ksudu94?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这是关于 3.7 版中引入的 TypeScript 特性:

[https://dev blogs . Microsoft . com/typescript/announcing-typescript-3-7-beta/](https://devblogs.microsoft.com/typescript/announcing-typescript-3-7-beta/):

```
let x = foo?.bar.baz();
```

在过去，当`foo`不是包含`bar`的有效对象时，我们需要添加一些额外的代码来保护逻辑，因为否则，我们根本无法将`foo`与`undefined`或`null`赋值。能够在空对象和填充对象之间切换对我们来说非常有用。举个例子，

```
let user = undefined;
setTimeout(() => {
  user = { name: "Fang" }
}, 5000);// Could be problematic depends on 
// when you invoke the following
user.name
```

我们需要在用户 5 秒钟后登录时填充用户，上面的测试代码很好地展示了这一点。如果没有新的可选链接，我们将需要显式添加一个`if`语句:

```
if (user) { 
  // access user properties
}
```

使用可选的链接，您可以避免编写`if`语句，或者至少隐藏该语句，稍后您将会看到:

```
const name = user?.name
```

## 惊人的功能？

任何节省开发人员时间的特性都是令人惊奇的特性，只要它能节省您的时间。因此，让我们看看该行做了什么，根据文档，它直接翻译为:

```
const name = (user === null || user === undefined) ? 
      undefined : 
      user.name
```

令人惊奇的是，比较有和没有可选链接的版本，我们将投票支持新语法。谁他妈的想一直写`user === undefined`？

现在开发人员发现这个新功能非常容易使用，他们开始为之疯狂。他们指责我们使用了`&&`，但他们倾向于写下如下内容:

```
const firstName = user?.name?.firstName;
```

上面的行基本上转化为下面的函数:

```
function getFirstName(user) {
  if (!user) return undefined
  if (!user.name) return undefined
  return user.name.firstName
}
```

哇，这不是很酷吗？你可能会说，“是的，这么少的代码做了这么多。”太神奇了，如果所有的编码都可以这样做，我们都可以退休了。

## 怎么了?

当然，我听起来不同意大众的观点。上面简单的代码会出什么问题呢？问题是你用`user?.name?.`代替了两个`if`语句。如果只有一个`if`语句，我们就会确切地知道是哪个`if`做出了返回`undefined`的决定。但是有了两个`if`，我们就不能再那样做了。但是你为什么想知道是哪个`if`做的决定？这是一个价值百万的问题。

也许这里使用可选链接的假设是，**你不应该想知道哪个** `**if**` **或者哪个空对象最后给了你空对象。不管出于什么原因，你想知道，你应该避免使用可选的链接。让我们来看一个例子，看看为什么:**

```
function Logo(user) {
  if (!user?.human) return 'Alien' return user?.name?.first
}
```

好的，你必须想象在我的代码深处我有一个组件`Logo`，它使用`user`对象，当然通常这个对象会作为*全局*类对象传递到这个组件中，但是为了这个对话，我们将把`user`直接传递给它。

`user?.human`的用法与`user?.name?.first`类似，因为我们想将`human`作为一个布尔值来做其他事情，例如返回一个`Alien`字符串。因此，在`user`对象之后有两个条件分支，`human`和`name`。在`name`之后，我们还有`first`。因此，如果你显式地编写上述组件，你可以说我们至少有四个`if`语句。好了，这个组件有什么问题？

我们必须假设`user`对象总是可用的。什么？我认为使用可选链接是为了避免知道这一点。例如，`user?.name?.`是总是获取`name`的完美用法(如果可用的话)。

是的，这是教科书上的原因。但事实并非如此，因为由于使用了上述语句中的`user?.human`,您仍然面临着空的和填充的两种选择。但是为什么另一个语句会破坏这种用法的语法呢？

让我们运行它，如果`user`不可用，`user?.human`就是`undefined`，因此它将返回`Alien`。是的，如果不是用户，他可以是一个`Alien`对不对？当然可以！问题不在于你是否幸运，而是你是否打算在那里做出这样的逻辑？你确定你不是在那里检查`user.human`(没有`?.`)吗？是吗？我的头在旋转，你有任何意义吗？

如果你有信心故意写下这句话，是的，我会让你通过。但如果没有，你的未来就注定了。问题是在写的时候你没有区分出`!user`和`!user.human`之间的区别。空用户和`human`设置为`false`的有效用户之间肯定有一些区别。你没发现问题吗？

我觉得我没必要太深入这个困境。因为我真的不认为这是值得解决的，因为几乎没有什么比意识到正确的陈述更能让你变得正确！你只需要确定你写的是你想要的，就这样。

我想说的是，太多的**(*)隐藏的***`**if**`**语句对你没有帮助，除非隐藏的版本在语义上 100%可翻译成精确的人类逻辑**。否则多一个隐藏的`if`只会让你的开发预算多一个零。

# 摘要

作为开发者工具，发明就是发明。不应该气馁。然而对于一个被锁住的隐藏`if`，我采取不同的态度。在函数式语言中，一个简化的隐藏的`if`不应该达到一个`Maybe`对象的高度。坚持那样做只会成为失败的圣经。因为`if`的数字，只会在你的代码深处的深层状态中，最后爆炸到任何人类都无法领悟的地步。

## 注意

您可能想知道编写上述代码的正确方法是什么:

```
function Logo(user) { 
  if (!user) return 'N/A' if (!user.human) return 'Alien' return user.name.first
}
```

上面的修正是有争议的，但是我采用了一个*极端的*方法，用一个显式的`if`语句替换所有的`?.`。你可能会称之为老学校，但这是防弹的，它在任何情况下都做我想做的事情。

当然，如果还没有解决，`user`可能不会出现在这个组件中，因此这将消除第一个`if`。是的，那会更正确。由于这需要一些架构上的改变，我将不再讨论它。

## 注 2

在这一点上，我有点确信可选链接的重要性堪比`&&`。我会随便用它作为一个技巧来回避局部的问题，而不是依赖它作为一个架构目的的全局策略。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***