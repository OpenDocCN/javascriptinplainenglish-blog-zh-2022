# JavaScript 中的类简介

> 原文：<https://javascript.plainenglish.io/an-introduction-to-classes-in-javascript-610eb442ae0e?source=collection_archive---------14----------------------->

## 如何创建和使用类，以及在使用它们时可能会遇到的一些常见问题。

![](img/9dc39828cf58224090a80f8d38ef0bde.png)

Photo by [Brooke Cagle](https://unsplash.com/@brookecagle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是一种强大的语言，为开发人员提供了许多特性。这些特性之一是类。类允许您创建从其他对象继承属性的对象。在这篇博文中，我们将介绍如何创建和使用类，以及在使用它们时可能会遇到的一些常见问题。

## ES6 之前的 JavaScript 类

在 ES6 之前，JavaScript 没有基于类的继承模型。在 ES6 之前，如果您想创建一个从另一个对象继承属性的对象，您必须使用基于原型的继承。基于原型的继承比基于类的继承稍微复杂一点，一开始可能很难理解。

为了让面向对象编程对开发者来说更容易，ES6 引入了类。类是基于原型的继承之上的语法糖，它们使创建和使用对象变得更加容易。虽然您没有必要为了使用类而理解基于原型的继承，但重要的是要认识到，类语法只是简单的语法糖，并抽象出底层的基于原型的继承模型。

## 创建一个类

如果你有面向对象编程语言的经验，比如 Java 或 C++，用 JavaScript 创建类会有相似的感觉。类语法不仅是为了抽象一些基于原型的继承的复杂概念，也是为了让 JavaScript 更像其他面向对象的语言。

创建一个类很简单。使用 class 关键字，后跟类名。类名大写是一种惯例。然后，我们可以添加我们的构造函数。构造函数是一个特殊的函数，在创建类的实例时调用。它用于初始化我们的实例的属性。

```
class Book { constructor(title, author) { this.title = title; this.author = author; }}
```

在上面的例子中，我们创建了一个 Book 类。我们的 Book 类有两个属性:标题和作者。我们在构造函数中初始化这些属性。当我们创建 Book 类的一个实例时，将调用构造函数，并将 title 和 author 属性设置为我们传入的值。

在我们的构造函数中，`this` 关键字引用新创建的实例。

![](img/de34a01471c3e27bb42389b3044ac63e.png)

Photo by [Glenn Carstens-Peters](https://unsplash.com/@glenncarstenspeters?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 创建类实例

现在我们已经创建了 Book 类，让我们创建它的一个实例。

```
const harryPotterBook = new Book(“Harry Potter and the Sorcerer’s Stone”, “J.K. Rowling”);
```

在上面的例子中，我们已经创建了 Book 类的一个实例。为了创建一个类的实例，我们使用了 new 关键字。我们向构造函数传递了两个参数:“哈利·波特和魔法石”作为标题，“J.K .罗琳”作为作者。这些参数将被传递给我们的构造函数，并用于初始化 book 实例的 title 和 author 属性。

```
console.log(harryPotterBook)**/*** Book {title: ‘Harry Potter and the Sorcerer’s Stone’,author: ‘J.K. Rowling’}
***/**
```

## 类方法

除了属性，类还可以有方法。方法是与类实例相关联的函数。它们可用于执行与实例相关的操作或计算值。

让我们在 Book 类中添加一个方法，输出书籍的描述。

```
class Book { constructor(title, author) { this.title = title; this.author = author; } getDescription() { return `${this.title} was written by ${this.author}.`; }}
```

`this` 关键字指的是调用该方法的实例。在本例中，`this` 指的是我们的 harryPotterBook 实例。现在，我们可以在 book 实例上调用 getDescription 方法。

```
const harryPotterBook = new Book(“Harry Potter and the Sorcerer’s Stone”, “J.K. Rowling”);console.log(harryPotterBook.getDescription())// Harry Potter and the Sorcerer’s Stone was written by J.K. Rowling.
```

## 结论

类是您可以在 JavaScript 程序中使用的强大工具。它们允许开发人员编写可重用的代码，这是面向对象编程的关键组成部分。JavaScript 中的类使得创建和使用对象变得容易，并且它们抽象出了一些更复杂的基于原型的继承思想。

我希望你从这篇文章中学到了一些东西！祝你的编码面试好运！

[*更多内容尽在* ***说白了。报名参加我们的* ***免费每周简讯*** *。关注我们关于****Twitter****和****LinkedIn****。查看我们的* ***社区不和谐*** *加入我们的* ***人才集体*** *。***](https://medium.com/p/dcac2d547a9c/edit)