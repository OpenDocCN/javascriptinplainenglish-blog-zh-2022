# 关于编写 JavaScript 代码的 4 个令人不安的事实很少被提及

> 原文：<https://javascript.plainenglish.io/4-uncomfortable-truths-about-writing-javascript-code-that-are-rarely-talked-about-99fff5a7b4f3?source=collection_archive---------4----------------------->

## 只有有经验的开发人员才知道的真相

![](img/b388ca7932460c43fce8e801116f16a4.png)

Photo by [Madara Parma](https://unsplash.com/@madaratravels?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一个长名字通常代表一个不好的抽象。

开发人员终身处于维护模式。

了解这些令人不快的事实会让我们作为开发人员的生活更轻松。如果我们了解他们，我们会和平相处。

在这里，我提到了作为 JavaScript 开发人员应该知道的四个令人不安的事实。

# 1.命令式修正了命名问题

在简单的英语中，我们用祈使句来发出命令、警告或某种建议。

例如:

*《站起来》*

*“去那里”*

*《买新衣服》*

命令式可以轻松解决程序员选择正确名称的问题。

大多数时候，我们程序员努力为变量、函数和类选择正确的名称。

当我们对选择一个名字感到困惑时，我们有时会花大约一个小时来考虑它。

## 这就是你解决问题的方法

想象一下，你是一家公司的 CEO，你在给公司的员工下命令。作为首席执行官，你不能选择不直接传达你的信息的词语。

作为首席执行官，你被迫直接下达命令，没有任何糖衣。

在代码库中写任何名字时，使用 CEO 的直接性。

把自己当成一个一边写变量和函数名一边发号施令的 CEO。

1.  如果你正在编写一个函数，它的作用是删除一条消息，那么使用名字`removeMessage()`。
2.  如果函数的作用是获取 a 和 b 两个数之间的一个随机数，就用`random(a, b)`。
3.  如果一个功能的作用是删除停用的用户，您可以使用名称`removeDeactivedUsers()`。

## 使用祈使句时不要写长名字

使用命令形式时，不要让函数名太长。

假设你要写一个函数来帮助你购买一辆特定品牌和颜色的汽车。

如果您使用命令形式编写以下函数名:

```
buyRedCarOfParticularBrand();
```

上面的长名字会被有经验的程序员认为是不好的名字。

一个长名字通常代表一个不好的抽象。

当你输入这么长的名字时，你应该考虑一下，重新考虑写这个名字。

不要键入一个很长的名字，而是使用参数来表达汽车的所有特征:

```
buyCar({color: 'red',
brand: 'particular'});
```

当我们使用参数来表达函数时，代码看起来更干净，也更容易阅读。

[](/popular-lies-mediocre-developers-fall-for-that-destroy-their-career-6addbf887a2) [## 平庸的开发人员容易相信的谎言会毁掉他们的职业生涯

### 你应该忽略的有害编程技巧

javascript.plainenglish.io](/popular-lies-mediocre-developers-fall-for-that-destroy-their-career-6addbf887a2) 

# 2.开源实现了你所有的 JavaScript 梦想

当开始学习编程时，每个开发人员都梦想着为像谷歌、微软、Meta(脸书)或网飞这样的公司工作。

这些大型科技公司的工作机会有限。不是所有的开发者都有机会为这些公司工作。

每个开发者为这些公司工作的梦想并没有实现。

唯一的原因就是供给和需求。与这些公司提供的工作相比，市场上的开发人员数量更多。

与著名的技术公司相比，一个开发人员为汽车、石油或保险公司工作的可能性很大。

为这些公司工作的开发人员有许多未实现的梦想。他们想从事他们梦想中的技术项目。

在他们的日常工作中，没有多少令人兴奋的项目在进行。这就是开源可以帮助他们的地方。

有成千上万的开源项目。

每个开源项目都需要这样或那样的支持。

如果你是一个没有参与你梦想中的科技项目的开发者，你应该寻找有趣的开源项目。

选择您想要贡献的梦想 JavaScript 堆栈，并开始为这些开源项目之一做出贡献。

## 以下是一些例子:

*   你可以选择平均技术堆栈。由 MongoDB(无 SQL 数据库)、Express.js(后端 web 框架)、Angular(前端框架)、Node.js(服务器端 JavaScript)组成。
*   你可以选择 MERN 理工大学。由 MongoDB(无 SQL 数据库)、Express(后端 web 框架)、React(前端框架)、Node.js(服务器端 JavaScript)组成。
*   MEVN 技术栈。由 MongoDB(无 SQL 数据库)、Express(后端 web 框架)、Vue.js(前端框架)、Node.js(服务器端 JavaScript)组成。
*   MEEN 理工大学。由 MongoDB(无 SQL 数据库)、Express(后端 web 框架)、Ember.js(前端框架)、Node.js(服务器端 JavaScript)组成。

开源 JavaScript 项目可以实现你未实现的 JavaScript 梦想。

[](/9-disruptive-react-libraries-nobodys-talking-about-4699034dd506) [## 没有人谈论的 9 个破坏性反应库

### 这些库将为 Web 开发人员的生活增加巨大的价值

javascript.plainenglish.io](/9-disruptive-react-libraries-nobodys-talking-about-4699034dd506) 

# 3.不解决债务问题将带来未来的噩梦

如果截止日期临近，我们需要编写大量代码，我们会这样做:

*   我们不再写有意义的名字。
*   即使有必要，我们也不写评论。
*   我们编写重复的代码。
*   我们不再担心文档。

作为开发人员，通过承担“技术债务”，我们按时完成任务。我们常说债务会在下一次迭代中处理。

在下一次迭代中，我们被不同的 bug 集合所包围。我们更关心当前的问题，而不是担心过去欠下的债务。

随着每一次迭代，你不断承担技术债务，在几次迭代之后，你的代码看起来就像垃圾一样。你会发现自己处于这样一种境地:要做出一个改变，你必须处理过去所有的债务。

你没有时间一次性解决所有的技术债务。噩梦开始了。

## 这些是技术债务的一些例子

*   开发人员选择他或她知道的工具，而不是选择正确的工具来完成工作。
*   当截止日期临近时，开发人员会忽略最佳实践和代码审查标准。最终会导致代码质量问题。尽可能快地行动会导致未来的问题。
*   当我们不使用有意义的名字时，技术债务就产生了。

不是像这样写一个函数:

```
function getUserInfo(name){ //do what you want}
```

您编写了这样的函数:

```
function gui(name){ //do what you want}
```

长此以往，没有人能够理解`gui` 函数在代码库中的作用是什么。

作为一名开发人员，当你承担了太多的技术债务时，你的代码质量就会下降。

尽早解决它通常更好。

# 4.“部署后开始维护”这句话是废话

低效的开发者认为，应用发布后，维护阶段就开始了。

这完全是谎言。

我们程序员总是处于维护模式。

与客户的一次会面或者仅仅是与合适的用户的一次交谈就可以改变需求。

现实世界在不断变化和发展。你今天对某事的了解会在两天后改变。

可能会收到需要快速创建的新功能的请求，而您已经开发了几个月的旧功能可能不再需要了。

任何时候都有必要对代码库进行小的或大的修改。

## 您不应该做的事情，因为我们始终处于维护模式

*   你不应该写耦合代码。如果你的代码包含高度耦合的元素，那么要做一个小的改变，你必须重写一些东西。
*   你不能重复你自己。如果您的代码包含重复的代码，那么要做一个小的改变，您需要在多个地方进行改变。
*   函数和类不应有一个以上的责任。拥有一个以上的职责会使函数和类的规模变得很大，并且您将无法轻松地进行所需的更改。

# 摘要

1.  使用祈使句。
2.  开源将满足你的所有需求。
3.  尽快解决技术债务。
4.  我们总是处于维护模式。

[](https://sanjay-priyadarshi.medium.com/meet-a-programmer-who-turned-an-open-source-platform-into-a-7-500-000-000-company-645e14c53c8) [## 遇到一个程序员，他将一个开源平台变成了一家价值 75 亿美元的公司

### 激励年轻程序员的旅程

sanjay-priyadarshi.medium.com](https://sanjay-priyadarshi.medium.com/meet-a-programmer-who-turned-an-open-source-platform-into-a-7-500-000-000-company-645e14c53c8) [](https://sanjay-priyadarshi.medium.com/a-19-year-old-programmer-dropped-out-of-college-to-build-a-2-300-000-000-company-in-2-years-1055963ec1db) [## 一名 19 岁的程序员从大学辍学，在两年内创建了一家价值 23 亿美元的公司

### 没有人能预料到他的成功

sanjay-priyadarshi.medium.com](https://sanjay-priyadarshi.medium.com/a-19-year-old-programmer-dropped-out-of-college-to-build-a-2-300-000-000-company-in-2-years-1055963ec1db) 

# 你想加速你的程序员生涯吗

加入一群热爱编程和技术的人。

[可以在这里加入。](https://codertoentrepreneurs.substack.com/)

在我们社区的帮助下，我们将解决程序员生活中的主要问题，并讨论前端和后端工程。

我们将帮助你重新规划你对科技中各种事物的理解。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***