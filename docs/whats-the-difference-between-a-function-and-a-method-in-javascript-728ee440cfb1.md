# JavaScript 中的函数和方法有什么区别？

> 原文：<https://javascript.plainenglish.io/whats-the-difference-between-a-function-and-a-method-in-javascript-728ee440cfb1?source=collection_archive---------5----------------------->

![I](img/41ad8cfea311ab834bb5281f53e0af44.png) 我 最近和一位开发伙伴进行了一次讨论。在讨论中，我注意到他混淆了函数和方法。如果你至少是一个中级软件工程师，这是一个你必须知道的话题。如果你不知道其中的区别，那么我建议你称自己为初级开发人员，继续阅读，因为这篇文章将用通俗易懂的语言向你解释 JavaScript 中方法和函数的区别。

这只是众多关于 JavaScript 和软件开发的文章中的一篇。欢迎关注我们，获取更多关于 JavaScript 和软件开发的精彩内容。我们尝试一周发布多次。请确保不要错过我们的任何精彩内容。

![](img/002ff94e9aca8a7e41956cb58a363a1d.png)

Photo by [Alejandro Piñero Amerio](https://unsplash.com/@vjgalaxy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，函数是一个代码块，可以定义，然后通过名称调用。可以使用 function 关键字定义一个函数，并且可以使用其名称后跟一组括号来调用它。函数可以定义为独立的代码块，也可以作为方法与对象相关联。

下面是 JavaScript 中一个独立函数的例子:

```
function greet(name) {
  console.log('Hello, ' + name + '!');
}
greet('John'); // Output: "Hello, John!" 
```

另一方面，方法是与对象相关联的函数。在 JavaScript 中，对象可以有属性和方法，属性是与对象相关联的值，方法是与对象相关联的函数。方法的调用方式与函数相同，但它们是在对象上调用的，使用点符号。

下面是 JavaScript 中的一个方法示例:

```
const person = {
  name: 'John',
  greet: function() {
    console.log('Hello, ' + this.name + '!');
  }
};

person.greet(); // Output: "Hello, John!" 
```

在本例中，greet 方法是一个与 person 对象相关联的函数。使用点符号在 person 对象上调用它，this 关键字引用 person 对象本身。

![](img/e0f90aa8a73ed83a7684ec0b22f6f292.png)

因此，总而言之，JavaScript 中函数和方法的主要区别在于，函数是独立的代码块，而方法是与对象相关联并在该对象上调用的函数。

写这篇文章的时候，我们收到了一条评论，说这篇文章是“贬低”。虽然它是以一种“尖锐”的方式写的(至少我们试图这样写)，但它肯定没有任何贬低的意思。我们在知识上都有差距，而且不是每个人都知道所有的事情。连“资深开发者”都算不上。这没关系，只要我们努力缩小差距。我们希望像这样的文章以及我们已经发表和即将发表的许多其他文章将有助于缩小这些差距。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

太简单了，伙计们。现在，我敢肯定你永远不会混淆这两者。如果你喜欢这篇文章，那么别忘了分享，鼓掌，关注我们。我们每周发表多篇文章。所以，不要错过任何一个。再见

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*