# JavaScript 中的单例模式

> 原文：<https://javascript.plainenglish.io/singleton-pattern-in-javascript-df47826ea4fc?source=collection_archive---------5----------------------->

![T](img/97e826c971e9cf5664ff0bfa07877590.png)  T 何 singleton 模式可能是软件工程中最著名的模式之一。但你知道这到底是怎么回事吗？在这篇文章中，我将用简单易懂的语言向你解释什么是单例模式，它的优点和缺点，以及单例模式的常见用例。

![](img/1bdda87b4cf61bd98ce4930e107e11f2.png)

Photo by Waldemar Brandt on Unsplash

Singleton 模式是一种设计模式，它确保只创建一个对象的实例，提供对该对象的全局访问点。在只有一个对象实例很重要的情况下，例如管理数据库连接或处理用户身份验证时，这很有用。

要在 JavaScript 中实现 Singleton 模式，通常需要创建一个类来表示要创建单个实例的对象。这个类将有一个私有构造函数，它防止其他代码直接创建该类的新实例。该类还会有一个静态方法，返回对象的单个实例。这个方法将首先检查对象的实例是否已经存在，如果不存在，它将创建一个新的实例并返回它。对该方法的后续调用将始终返回该对象的同一个实例，从而确保只创建一个实例。

下面是一个如何在 JavaScript 中实现单例模式的例子:

```
class DatabaseConnection {
  // Private constructor
  constructor() {
    // Code to create a database connection
  }

  // Static method to get the single instance of the object
  static getInstance() {
    // Check if an instance already exists
    if (!DatabaseConnection.instance) {
      // If not, create a new instance
      DatabaseConnection.instance = new DatabaseConnection();
    }
    // Return the instance
    return DatabaseConnection.instance;
  }
} 
```

要使用该类，其他代码将调用 getInstance()方法来获取 DatabaseConnection 对象的单个实例。然后，可以使用该实例对数据库执行操作，例如执行查询或关闭连接。

在 JavaScript 中使用单例模式的优点包括:

*   它确保只创建一个对象实例，这在只有一个对象实例很重要的情况下很有用，例如管理数据库连接或处理用户身份验证。
*   它提供了对对象的单个实例的全局访问点，允许其他代码轻松访问和使用该对象。
*   通过允许代码的不同部分共享和重用对象的单个实例，它可以帮助提高应用程序的性能。
*   通过集中管理对象的单个实例，它有助于降低应用程序的复杂性。

然而，单例模式也被认为是一种反模式，也就是说，如果有其他选择，就不应该实现它。以下是一些缺点:

*   它会使应用程序更难测试，因为对对象的单个实例的全局访问使得用 mock 或 stub 替换对象以进行测试变得困难。
*   这会使应用程序更难维护，因为对对象的单个实例的全局访问意味着对对象的更改可能会影响代码的其他部分。
*   这会降低应用程序的灵活性，因为对象的单个实例是在应用程序初始化时创建的，在运行时不容易更改或替换。
*   这会降低应用程序的模块化程度，因为对象的单个实例与代码的其余部分紧密耦合，不能在其他应用程序中轻松重用。

然而，JavaScript 中有几个单一模式的常见用例，包括:

*   管理数据库连接:Singleton 模式可用于确保只创建数据库连接的一个实例，提供对该连接的全局访问点。这对于避免创建到同一个数据库的多个连接的开销，以及使代码的不同部分容易访问数据库是很有用的。
*   处理用户身份验证:Singleton 模式可用于确保只创建一个用户身份验证管理器的实例，提供对该管理器的全局访问点。这有助于避免创建多个身份验证管理器的开销，并使代码的不同部分易于对用户进行身份验证。
*   缓存数据:Singleton 模式可用于确保只创建一个数据缓存实例，提供对该缓存的全局访问点。这有助于避免创建多个数据缓存的开销，并使代码的不同部分易于访问缓存的数据。
*   管理应用程序设置:Singleton 模式可用于确保只创建应用程序设置管理器的一个实例，提供对该管理器的全局访问点。这有助于避免创建多个设置管理器的开销，并使代码的不同部分易于访问和更新应用程序设置。
*   实现记录器:Singleton 模式可用于确保只创建一个记录器实例，提供对该记录器的全局访问点。这有助于避免创建多个记录器的开销，并使代码的不同部分易于记录消息和事件。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

请继续关注我，因为我将在接下来的文章中发布更多关于 JavaScript 设计模式的内容。这里是我将要介绍的 JavaScript 中所有[设计模式的概述。](https://pandaquests.medium.com/overview-of-design-patterns-in-javascript-27d14530397a)

你有什么问题吗？你以前用过单例模式吗？用例是什么，为什么你选择了单例模式而不是另一个解决方案？让我知道并在下面评论。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***