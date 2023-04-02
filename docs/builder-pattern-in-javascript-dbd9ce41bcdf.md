# JavaScript 中的构建器模式

> 原文：<https://javascript.plainenglish.io/builder-pattern-in-javascript-dbd9ce41bcdf?source=collection_archive---------9----------------------->

![H](img/2cd81f425c86f0481dd2c5dcbd3e452c.png)  H   ey 那里！你是否厌倦了在 JavaScript 中不断编写重复的构造函数和工厂函数来创建对象？不要害怕，因为构建器模式是来拯救世界的！有了这个强大的设计模式，您将能够轻松地创建具有您需要的所有附加功能的复杂对象，而不必编写大量的样板代码。所以，拿起你最喜欢的饮料，坐下来，让我们一起进入构建者模式的世界吧！

![](img/f9a421c8c100d14304885251903ba859.png)

Photo by [Marcel Strauß](https://unsplash.com/@martzzl?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

构建器模式是一种设计模式，允许您以循序渐进的方式创建复杂的对象。当您想要创建一个具有许多不同属性或特征的对象，并且不希望一次指定所有属性或特征时，它特别有用。

假设您想用 JavaScript 创建一个汽车对象。汽车可能具有汽车的构造和型号、汽车的颜色、车门的数量等属性。如果没有生成器模式，您可能需要创建一个单独的构造函数，将所有这些属性作为参数，如下所示:

```
function Car(make, model, color, doors) {
 this.make = make;
 this.model = model;
 this.color = color;
 this.doors = doors;
}
const myCar = new Car('Ford', 'Mustang', 'red', 4);
```

如果您只需要创建几种不同类型的汽车，这种方法会很好，但是如果您需要创建许多不同类型的具有许多不同属性的对象，这种方法会变得很笨拙。

使用构建器模式，您可以创建一个单独的“构建器”对象，该对象将指导您逐步完成创建对象的过程。您可以一次设置一个属性，如下所示:

```
function CarBuilder() {
 this.make = '';
 this.model = '';
 this.color = '';
 this.doors = 0;
 this.setMake = function(make) {
   this.make = make;
   return this;
 }
 this.setModel = function(model) {
   this.model = model;
   return this;
 }
 this.setColor = function(color) {
   this.color = color;
   return this;
 }
 this.setDoors = function(doors) {
   this.doors = doors;
   return this;
 }
 this.build = function() {
   return new Car(this.make, this.model, this.color, this.doors);
 }
}
const carBuilder = new CarBuilder();
const myCar = carBuilder
 .setMake('Ford')
 .setModel('Mustang')
 .setColor('red')
 .setDoors(4)
 .build();
```

起初，这可能看起来像是很多代码，但是从长远来看，它可能更容易使用和更灵活，特别是如果您需要创建具有许多不同属性的许多不同类型的对象。
构建器模式有几个优点:

*   它允许您逐步创建复杂的对象，而不必一次指定对象的所有属性。这可以使理解和使用代码变得更容易，尤其是当您使用许多不同的属性时。
*   它允许您通过只设置您需要的属性来创建对象的不同“风格”。例如，您可以使用同一个构建器创建一辆手动变速器汽车和一辆自动变速器汽车，只需设置不同的属性。
*   它可以使您的代码更加灵活和可重用。您可以使用同一个生成器来创建不同类型的对象，并且可以在代码的不同部分使用它，而不必编写大量的样板代码。

然而，构建器模式也有一些缺点:

*   它可能需要更多的代码来实现，尤其是当您使用许多不同的属性时。
*   这使得理解不同对象之间的关系变得更加困难，因为这些对象是逐步创建的，而不是一次性创建的。
*   调试可能会更加困难，因为对象是逐步创建的，而不是一次性创建的。

构建器模式在某些情况下可能是一个有用的工具，但是在使用它之前考虑它是否适合您的项目是很重要的。当您需要创建具有许多不同属性的复杂对象时，构建器模式是 JavaScript 中最常用的。以下是几个何时可以使用构建器模式的示例:

*   当您处理大量可选参数时。如果您有一个带有许多可选参数的构造函数，那么 Builder 模式允许您单独设置每个参数，从而使您更容易理解和使用您的代码。
*   当你需要为一个对象创造不同的“风格”时。例如，如果您正在创建一个汽车对象，您可能需要创建不同版本的汽车，具有不同的引擎大小、传动类型和其他属性。构建器模式允许您通过仅设置您需要的属性来轻松地创建这些不同版本的对象。
*   当您希望保持代码的灵活性和可重用性时。构建器模式允许您使用同一个构建器创建不同类型的对象，这可以使您的代码更加灵活，更容易在项目的不同部分重用。
*   当您希望避免创建大量样板代码时。如果您需要创建许多具有不同属性的不同对象，构建器模式可以帮助您避免编写大量重复的代码来创建这些对象。

因此，总而言之，每当您需要创建具有许多不同属性的复杂对象时，构建器模式都是一个有用的工具。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

感谢您阅读关于构建器模式的内容！我们希望这些信息对您有所帮助，并希望您在自己的项目中使用这种设计模式时更有信心。如果您对构建器模式有任何问题或评论，或者如果您想了解更多关于其他设计模式的信息，我们鼓励您在下面留下您的评论。

此外，如果你想了解我们未来关于设计模式的帖子(这里是我们将要涉及的 JavaScript 中所有[设计模式的概述)和软件开发中的其他主题，请务必关注并订阅我们的 medium。我们总是分享有用的提示和信息，我们希望您加入我们的软件开发人员社区。](https://medium.com/@pandaquests/overview-of-design-patterns-in-javascript-27d14530397a)

再次感谢您的阅读，祝您编码愉快！

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***T21](https://www.linkedin.com/company/inplainenglish/)*[**YouTubeT30**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*和**[**T40**](https://discord.gg/GtDtUAvyhW)**不和****

## **想扩大你的软件创业规模吗？查看[电路](https://circuit.ooo/?utm=publication-post-cta)。**