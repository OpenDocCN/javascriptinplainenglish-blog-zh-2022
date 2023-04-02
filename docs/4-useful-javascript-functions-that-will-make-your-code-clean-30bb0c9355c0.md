# 4 个有用的 JavaScript 函数将使你的代码变得干净

> 原文：<https://javascript.plainenglish.io/4-useful-javascript-functions-that-will-make-your-code-clean-30bb0c9355c0?source=collection_archive---------7----------------------->

## 让你的代码看起来更干净、更简短、更容易理解

![](img/cfe00e0e504c8d314e8d861cf13f286f.png)

Photo by [mari lezhava](https://unsplash.com/@marilezhava?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在使用循环时，JavaScript 拥有多种函数。JavaScript 数组有许多函数，它们提供了一种更简单、更有效的方式来表达逻辑。这些函数帮助我们编写更简单、更容易理解的代码。

有时候，这些函数比普通的`for`循环要高效得多。一些函数为一些逻辑操作提供了意义，因此对程序员来说可读性更强。这就是为什么我们要掌握 JavaScript 中可以作为`for`循环替代的基本函数。

所以，事不宜迟，让我们看看 JavaScript 中的一些基本函数，它们可以用来替代`for`循环。

# 1.发现

`find()`通常用于查找与给定表达式匹配的元素。

**场景:**假设，我们只需要找到一个年收入大于或等于$50k 的用户。我们可以使用下面的代码来获得这样的资格用户。

(❌坏)

(✅好)

看到区别了吗？当然，后者看起来要短得多，也可以理解。

# 2.过滤器

`filter()`函数返回一个匹配给定表达式的数组。

**场景:**假设，这一次，我们想要获取所有年收入至少为 50k 美元的用户。

(❌坏)

(✅好)

# 3.地图

`map()`通常用于根据给定的列表和逻辑得到另一个数组。

**场景:**假设，我们想从给定的名和姓中获取用户的全名。此外，我们希望从用户的生日中获取年龄。下面的代码块可以解决我们的问题。然而，后者更容易理解，效率也更高。

(❌坏)

(✅好)

# 4.减少

`reduce()`函数用于根据数组计算一些值，例如，所有雇员的总收入、列表中一些属性的总和等。

**场景:**假设，我们想计算用户的总年收入。我们可以使用`reduce`函数轻松地将所有用户的年收入相加，这将比使用普通的`for`循环更容易理解。

(❌坏)

(✅好)

# 最后的想法

通过分析上面的代码，我们可以肯定地说,`for`循环的这些替代方法对人眼来说可读性更强，更集中，更容易理解。

然而，`for` loop 并不总是那么糟糕。有时候，在我们的 web 工程项目中，我们需要处理一些复杂的查询，即使我们不愿意，也必须使用`for`循环。

但是如果我们知道这些方法，我们肯定可以节省时间和精力来编写更少、更干净、更有组织的代码。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和****[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**