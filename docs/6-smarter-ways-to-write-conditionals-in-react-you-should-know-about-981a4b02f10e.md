# 你应该知道的在 React 中写条件句的 6 种更聪明的方法

> 原文：<https://javascript.plainenglish.io/6-smarter-ways-to-write-conditionals-in-react-you-should-know-about-981a4b02f10e?source=collection_archive---------3----------------------->

## 每个开发人员都应该知道的 6 个 React 技巧。

![](img/3d60d518a6015bab370e8fadf27c0517.png)

Photo by [Steve Tsang](https://unsplash.com/@stevetsang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 那是一个可怕的问题

在 React 中，我们经常编写条件语句来显示不同的视图，就像这个简单的例子。

但是当项目的代码规模足够大并且有很多 JSX 条件句时，事情会很快失去控制。**代码变得极其混乱，可读性差。**

就像下面这段代码，我真的没有勇气和信心去了解它的细节…

**那么在 React 中，我们有什么方法可以写出更易读、更易维护的代码呢？**

# 1.使用三元运算符

三元运算符更适合需要少量条件判断的场景。

如果有很多条件分支，就会发生上面例子的灾难。

例如，要在移动设备上显示一个`Mobile`组件，而在其他屏幕上显示另一个组件，您可以使用三元表达式来实现:

# 2.使用“&&”简化三元运算符

有时候我们可以用“&&”来简化三元表达式，比如下面的代码。

**& &**

为什么要用两个感叹号把**显示的**转换成布尔值？欢迎你查看我的[其他文章](/my-boss-you-dont-know-react-at-all-f493970f1807)，里面有非常详细的说明。

# 3.使用“如果”语句

如果有数据，则显示`List`组件。如果没有数据，则不显示任何内容。使用`if`语句也是一个不错的选择。

当然，发送请求并不总是成功，也可能失败。我们可以添加一些`if`分支来控制不同的逻辑。

# 4.使用“开关”

太多的`if`语句会导致组件混乱。可以将多个条件提取到包含`switch`语句的单独组件中。

让我们来看看一个简单的菜单切换组件:

你可以看到使用‘switch’可以很容易的表达‘menu’和组件的对应关系。

# 5.使用枚举

如果我们需要根据用户的不同状态显示三个组件`Foo`、`Bar`、`Default`，枚举会比`if`语句更优雅。

# 6.使用 JSX 控制语句

JSX 控制语句库扩展了 JSX 的功能，这样你就可以直接使用 JSX 来实现条件渲染。

我们举个例子。

# 最后

**感谢阅读。**我期待期待您的关注和阅读更多高质量的文章。

[](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [## “我失去了一个工作机会，只是因为承诺。所有”

### 一次让我好难过的面试经历。

javascript.plainenglish.io](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) [## 现在是 2022 年，不要再滥用箭头功能了

### 不应该使用箭头函数的 4 种情况。

javascript.plainenglish.io](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*