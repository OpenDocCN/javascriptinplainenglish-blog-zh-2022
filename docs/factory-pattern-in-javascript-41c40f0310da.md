# JavaScript 中的工厂模式

> 原文：<https://javascript.plainenglish.io/factory-pattern-in-javascript-41c40f0310da?source=collection_archive---------10----------------------->

![H](img/2cd81f425c86f0481dd2c5dcbd3e452c.png)  H 你听说过 JavaScript 中的工厂模式吗？在这篇文章中，我将向你解释一些容易理解的词语。本文是我撰写的关于 JavaScript 设计模式的系列文章的一部分。这里是我将要介绍的 JavaScript 中所有[设计模式的概述。](https://pandaquests.medium.com/overview-of-design-patterns-in-javascript-27d14530397a)

![](img/ba7b23dda59694319a5def2e921da144.png)

Photo by Allan Wadsworth on Unsplash

工厂模式是 JavaScript 中的一种设计模式，它提供了一种创建对象的方法，而无需指定将要创建的对象的确切类。当您想要创建属于特定类家族的对象，但不想指定将在运行时创建的对象的确切类时，这是很有用的。

要在 JavaScript 中实现工厂模式，您需要定义一个函数(工厂函数),它接受一些参数并返回一个对象。返回的对象通常是一个类的实例，但是工厂函数本身并不指定将要创建的对象的确切类。相反，它根据提供的参数确定要创建的对象的类别。

例如，考虑一个简单的工厂函数，它创建表示不同形状的对象。工厂函数采用类型参数，确定要创建的形状的类型。根据类型参数，工厂函数可能返回 Circle 类、Square 类或 Triangle 类的实例。

```
function createShape(type) {
  if (type === 'circle’) {
    return new Circle();
  } else if (type === 'square’) {
    return new Square();
  } else if (type === 'triangle’) {
    return new Triangle();
  }
} 
```

在此示例中，createShape 函数充当创建不同形状的工厂。它接受类型参数并使用它来确定实例化哪个对象类。这允许 createShape 函数的调用方在不知道将要创建的对象的确切类别的情况下创建对象。

工厂模式非常有用，因为它允许您创建对象，而无需指定将要创建的对象的确切类别。这使得您的代码更加灵活和易于维护，因为您可以添加新类型的对象，而无需修改使用工厂函数的现有代码。

工厂模式有几个优点，包括:

*   它允许您创建对象，而无需指定将要创建的对象的确切类别。这使得您的代码更加灵活和易于维护，因为您可以添加新类型的对象，而无需修改使用工厂函数的现有代码。
*   它促进了创建对象的代码和使用这些对象的代码之间的松散耦合。这使得您的代码更加模块化，更易于测试，因为使用这些对象的代码不需要知道将要创建的对象的确切类。
*   它允许您抽象出对象创建的细节，使您的代码更容易理解和维护。

但是，工厂模式也有一些缺点，包括以下几点:

*   它可以使你的代码更加复杂，因为它增加了一个额外的抽象层。这可能会增加理解和调试代码的难度。
*   这使得预测代码的行为变得更加困难，因为工厂函数决定了将在运行时创建的对象的类。
*   这会降低代码的效率，因为工厂函数必须确定运行时要创建的对象的类。这可能会增加开销并降低性能。

总的来说，工厂模式有一些有用的好处，但是它也有一些缺点。在特定情况下是否使用工厂模式取决于具体的需求和所涉及的权衡。

工厂模式通常用于希望创建属于某个特定类家族的对象，但不希望指定将在运行时创建的对象的确切类的情况。工厂模式何时有用的一些常见示例包括:

*   当您想要创建表示不同形状类型(如圆形、正方形和三角形)的对象时。工厂函数可以接受类型参数，并返回适当的 shape 类的实例。
*   当您想要创建表示不同类型汽车的对象时，例如轿车、掀背车和 SUV。工厂函数可以接受类型参数，并返回适当的 car 类的实例。
*   当您想要创建代表不同类型的雇员(如经理、工程师和销售人员)的对象时。工厂函数可以接受类型参数，并返回适当的雇员类的实例。

在每个例子中，工厂模式允许您创建对象，而无需指定将要创建的对象的确切类。这使得您的代码更加灵活和易于维护，因为您可以添加新类型的对象，而无需修改使用工厂函数的现有代码。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

请继续关注我，因为我将在接下来的文章中发布更多关于 JavaScript 设计模式的内容。这里是我将要介绍的 JavaScript 中所有[设计模式的概述。](https://pandaquests.medium.com/overview-of-design-patterns-in-javascript-27d14530397a)

你以前用过工厂模式吗？你的经历是什么？请在下面评论并告诉我们。关注更多高质量和易于理解的文章。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***