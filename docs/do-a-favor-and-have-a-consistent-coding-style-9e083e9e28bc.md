# 帮个忙，保持一致的编码风格

> 原文：<https://javascript.plainenglish.io/do-a-favor-and-have-a-consistent-coding-style-9e083e9e28bc?source=collection_archive---------15----------------------->

## 持续的坏比持续的好要好。

![](img/da9d8329413ccc5ea619d0c59689674b.png)

Photo by [Louis Hansel](https://unsplash.com/@louishansel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编写代码很棘手。

你可以搞砸很多事情。您可能会犯一些语法错误，不能正确传递数据，或者逻辑错误。

见鬼，如果您错过了甚至一个分号，它将不会工作。

**编写可读的代码更加困难。**

您可以进行大量的练习，并学习如何正确地使用逻辑、框架和库。

电脑很开心。它理解你的代码并能执行它。但是人类呢。如果你有混乱的代码，没有人(通常是你)能正确地阅读和理解你的代码。

这个问题比你想象的更重要。

初级开发人员在他们只专注于让某些东西工作的早期会犯这种错误。

他们看不到长远的前景，有人会在他们之后从事相同的代码库工作。他们完成工作后继续前进。然而，只要遵循一个原则，您就可以编写可读和可维护的代码。

> *一致性。*

一致性是我最喜欢的编程原则之一。

我发现拥有一致的编码风格更容易维护。它可以将你未来的自己从大量的挫折和头痛中拯救出来。你可以很容易地阅读和理解它。

大型代码库中没有一致性对于任何新开发人员来说都是一场噩梦。

# 风格一致性

代码应该看起来像是一个人写的。

不同的编程语言、框架和团队都有自己的风格指南。在编写代码之前阅读这些指南总是有好处的。

他们可以让你的代码变得更好。

*比如，*假设我有一个数组，里面有一些元素。我喜欢把每个元素写在不同的行上。我发现当每个元素都有自己的线条时，阅读起来会更容易。

```
notMyArray = ['longVarName', 'anotherLongVarName', 'thisIsCluttered'] myStyledArray = [
  'longVarName',
  'anotherLongVarName',
  'thisIsEasierToRead',
]
```

当我们调用一个有很多参数的函数时，这一点更加突出。参数长度的变化会使其难以阅读。相反，将所有参数写在单独的行上可以使阅读更容易。

```
doesThisLookGood(param0=50000, param1='Hello World', param3=[1, 2, 3], param3=true) doesThisLookBetter(param0=50000,
                   param1='Hello World',
                   param2=[1, 2, 3],
                   param3=true)
```

# 一致命名

遵循命名约定至关重要。

不管你在做什么，你都应该有一个命名约定。不要在命名上重新发明轮子。想想你周围的人。

每个人都遵循一个命名约定，不管是编程，你的孩子，还是你的狗。你不能给你的狗取名叫“凯蒂”

## 按照惯例拿起骆驼箱或蛇箱。

根据你的语言习惯和你团队的风格准则来选择案例。

变量名应该表明它们是什么。它应该充分地捕获它所保存的数据。同样，函数的名字应该告诉他们正在执行的工作。

当你只看一眼它的名字就能知道它是什么的时候，这是很有帮助的。

## 相似地命名相关的变量、函数和类。

如果事物之间有关系，就表现出来。

例如，如果您有多个用户实例。不要为每个用户使用不同的变量名。遵循一致的方法。

```
// Bad Naming Style
u1 = 'John'
user2 = 'Kristian'
u3 = 'Aaron'// Good Naming Style
user1 = 'John'
user2 = 'Kristian'
user3 = 'Aaron'
```

不要害怕创建长变量名。如果它是有意义的，并且正确地传达了信息，它比一些不清楚的，简短的，花哨的名字要好。

## 文件名的一致性。

节省时间的最大诀窍之一是为文件取一个有意义的名字。

在较大的代码库中，有数百个不同的文件。一切都相互影响，找到特定的文件或函数变得很麻烦。

有一个一致的文件命名系统是很重要的，这样可以很容易地找到你要找的东西。

另一个重要的因素是有一个一致的文件目录系统，稍后会详细介绍。

# 结构一致性

任何软件都有一个等级体系。

有保存单一类型数据的小变量，也有执行某个特性的完整类和模块。在运行应用程序的过程中，一切都起着至关重要的作用。

程序员有责任对*进行结构一致的编码*。

假设您有一个从 API 获取数据、处理数据并格式化数据的函数。你可以在一个函数中写完整的代码，但是这太麻烦了。

```
function getFinalData () {
  // 5 lines of code to fetch data
  // 15 lines of code to process data
  // 2 lines of code to format data
}
```

一些开发人员可能会这样重构它—

```
function getFinalData () {
  fetchRawData()
  processData()
  // 2 lines of code to format data
}function fetchRawData () {
  // 5 lines of code
}function processData () {
  // 15 lines of code
}
```

请注意，这使得代码看起来更具可读性。但是，这里的问题是结构。格式化数据的两行代码是不同的抽象层次。

为了有一个一致的结构，你应该把代码放在同一个抽象层次上，不管组件的代码行有多长。

```
function getFinalData () {
  fetchRawData()
  processData()
  formatData()
}function fetchRawData () {
  // 5 lines of code
}function processData () {
  // 15 lines of code
}function formatData () {
  // 2 lines of code
}
```

在创建函数和类时，应该遵循适当的层次结构。你和你的读者会更容易找到东西。

# 文件目录一致性

无论何时开始一个项目，都是从少量的文件开始。但是，随着项目的增长，文件的数量也在不断增加。

如果你不遵循一致的文件目录，事情肯定会变得一团糟。

每当有人想要深入你的源代码，这肯定会破坏他们阅读你的代码的动机(包括你)。

你应该有一个适当的文件管理系统和你做的每个项目的指导方针。

在 ReactJS 中，我们将*组件*放在一个文件夹中，*钩子*放在另一个文件夹中，而*资产*放在另一个文件夹中。如果您不这样做，那么当您试图阅读您的代码时，肯定会产生很多令人头痛的问题。

编写可读的代码并不简单。这对初学者来说很难，有时甚至对经验丰富的开发人员来说也很难。

学习编程是一个终生的过程，随之而来的是如何让你的代码更具可读性。

如果你是新来的，喜欢这篇文章，在 Medium 上还有很多这样的文章。你可以注册阅读它们，每月只需 5 美元。

[**这里是无限制访问媒体上所有内容的链接。**](https://arpitfalcon.medium.com/membership) 如果您使用此链接注册，我将免费为您赚取一小笔费用。

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。**