# JavaScript 中的装饰模式

> 原文：<https://javascript.plainenglish.io/decorator-pattern-in-javascript-2bc094ee1718?source=collection_archive---------7----------------------->

![T](img/97e826c971e9cf5664ff0bfa07877590.png)  T 这是我们下一篇关于 JavaScript 中装饰模式的博文！我们计划用 JavaScript 写很多关于设计模式的文章。如果你是一个经验丰富的开发人员，你可能会想“哦，太好了，又一个无聊的设计模式讲座。”但是不要害怕，亲爱的读者！我们保证会增加趣味，让这本书变得有趣和吸引人。所以戴上你的装饰帽(或者围裙，如果那更适合你的风格)，让我们进入装饰者模式的世界。

![](img/f401d68a7d2f7d34574ab29948f0925a.png)

Photo by [laura adai](https://unsplash.com/@lauraadaiphoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

装饰模式是一种向现有对象添加新行为而不改变其代码的方式。这就像在圣代冰淇淋上加了一颗樱桃——它在原有的基础上增加了一些额外的东西，但圣代冰淇淋的核心还是一样的。

在 JavaScript 中，这可能看起来有点像向内置对象(如数组)添加一个新方法。假设我们想添加一个名为“shuffle”的方法，它随机地重新排列数组中的元素。我们可以这样使用装饰模式:

```
const array = [1, 2, 3, 4, 5];
// This is the "decorator" function that adds the new behavior
function addShuffleMethod(array) {
  array.shuffle = function() {
  // code to shuffle the array goes here
  }
  return array;
}
// We "decorate" the array by calling the decorator function
const decoratedArray = addShuffleMethod(array);
// Now we can use the new shuffle method on our decorated array
decoratedArray.shuffle();
```

装饰模式是一种在不改变对象代码的情况下向对象添加新功能的方式。它是一个有用的工具，可以以灵活和模块化的方式向现有对象添加额外的功能。装饰模式是软件工程中的一种设计模式，它允许你向现有对象动态添加新的行为。当您想要扩展类或对象的功能而不更改其代码时，这很有用。

在 JavaScript 中使用装饰模式有几个优点:

*   它允许您在运行时向对象添加新的行为，而不必修改对象的代码。这意味着您可以轻松地扩展对象的功能，而不必对对象的代码进行任何更改。
*   装饰模式通过将对象的核心功能与您想要添加的附加行为分离开来，有助于保持您的代码整洁有序。
*   装饰模式可用于向不同类的对象添加行为，只要它们实现相同的接口。这使得向各种对象添加新行为变得容易，而不必为每个对象创建新的子类。
*   装饰模式可用于在应用程序中轻松实现横切关注点，如日志记录或安全性。这些问题是应用程序中多个对象所需要的行为，装饰模式允许您轻松地将它们添加到所有相关对象中，而无需重复代码。
*   使用函数闭包可以很容易地在 JavaScript 中实现 decorator 模式，这允许您创建可用于包装其他函数或对象的 decorator 函数。这使得在不修改代码的情况下向对象或函数添加新行为变得容易。

但是请注意，在 JavaScript 中使用装饰模式有一些潜在的缺点:

*   decorator 模式会使您的代码更加复杂和难以理解，尤其是当您在应用程序中使用多个 decorator 时。这可能会增加维护和调试代码的难度。
*   装饰模式还会使理解应用程序中不同对象之间的关系变得更加困难。这使得跟踪数据流和理解应用程序的不同部分是如何组合在一起的变得更加困难。
*   装饰器模式也可能不如其他设计模式有效，尤其是当您在应用程序中使用多个装饰器时。这是因为每次使用装饰函数或对象时，都必须调用每个装饰函数，这会增加代码的开销。因此，对于高性能或时间关键的特性，不建议使用它。
*   装饰模式可能不是每种情况下的最佳选择。在某些情况下，使用继承或组合来扩展对象的功能可能比使用装饰模式更合适。
*   最后，装饰器模式可能不像其他设计模式那样广为人知或广泛使用，如果其他开发人员不熟悉该模式，他们会更难理解您的代码。

总的来说，装饰模式可以在 JavaScript 的各种情况下使用，为现有对象动态添加新的行为。以下是装饰模式的几个用例示例:

*   向对象添加额外的功能:您可以使用 decorator 模式向对象添加新的方法或属性，而无需更改对象的代码。如果您想在不修改对象核心功能的情况下扩展对象的功能，这将非常有用。
*   实现横切关注点:您可以使用 decorator 模式轻松地添加应用程序中多个对象所需的行为，比如日志记录或安全性。这有助于组织您的代码并避免重复。
*   包装现有对象:可以使用装饰模式包装现有对象或函数，并向其添加新行为。如果您想在不修改代码或创建子类的情况下扩展对象的功能，这将非常有用。
*   向不同类的对象添加行为:您可以使用 decorator 模式向不同类的对象添加新行为，只要它们实现相同的接口。如果您想向各种对象添加新行为，而不必为每个对象创建新的子类，这将非常有用。
*   向第三方库添加行为:您可以使用 decorator 模式向第三方库中的对象或函数添加新行为，而无需修改库的代码。如果您想扩展库的功能而不必派生库的代码，这可能很有用。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

感谢阅读！我们希望这篇关于设计模式的文章对你有所帮助和启发。如果你有任何问题或者想了解更多关于设计模式的知识，请在下面留下你的评论。我们喜欢收到读者的来信，我们会尽最大努力回答您的任何问题。

不要忘记关注我们，了解更多关于设计模式和其他软件工程主题的精彩内容。这里是我们将要涉及的 JavaScript 中所有[设计模式的概述。我们将很快发布更多帖子，请关注或订阅更多帖子！](https://pandaquests.medium.com/overview-of-design-patterns-in-javascript-27d14530397a)

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*