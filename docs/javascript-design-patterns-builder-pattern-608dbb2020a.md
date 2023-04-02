# JavaScript 设计模式:构建器模式

> 原文：<https://javascript.plainenglish.io/javascript-design-patterns-builder-pattern-608dbb2020a?source=collection_archive---------4----------------------->

## 从 ES6 重新连接 JavaScript 设计模式

![](img/146fae02395cebb612b2a9f113939b0f.png)

## 1.什么是构建器模式？

构建器模式将复杂对象的构造层与其表示层分离开来，以便同一构造过程可以使用不同的表示。

构建器模式的特点是一步一步地构建一个复杂的对象，该对象可以用不同的组合或具有不同含义的序列来构建。通常用户不需要知道构造的细节，通常使用链调用来执行构造过程，最后调用 build 方法来生成最终的对象。

工厂模式也用于创建对象，但如何创建并不重要。工厂模式关注的是创建的结果，而构建器模式不仅得到结果，还参与创建的具体过程，适合创建复杂的复合对象。

## 2.ES6 中的构建器模式

让我们假设一个出版商的图书后端输入系统的业务场景。书籍有四个必需的信息:标题、作者、价格和类别；我们想要创建一个 book 对象来返回到后端。让我们结合使用 ES6 语法和构建器模式，一步一步地创建对象。

```
 class BookBuilder {
  constructor() {
    this.name = '';
    this.author = '';
    this.price = 0;
    this.category = '';
  }

  withName(name) {
    this.name = name;
    return this;
  }

  withAuthor(author) {
    this.author = author;
    return this;
  }

  withPrice(price) {
    this.price = price;
    return this;
  }

  withCategory(category) {
    this.category = category;
    return  this;
  }

  build() {
    return {
      name: this.name,
      author: this.author,
      prices: this.price,
      category: this.category
    }
  }
}

//Calling the builder class
const book = new BookBuilder()
  .withName("The Reckonings")
  .withAuthor('Lacy Johnson')
  .withPrice(31)
  .withCategory('Literature')
  .build();
```

以上讲述了如何编写和调用 my `BookBuilder`的 creator 类，但仅仅是一个有 4 个属性的对象，我们就用了这么多代码来创建，远比直接在构造函数中传递参数来创建对象复杂。这是因为我们在创建过程中有太多的`withxxxx` 方法。我们实际上可以自动创建这样的`withxxxx` 方法来简化代码。

```
 class BookBuilder {
  constructor() {
    this.name = '';
    this.author = '';
    this.price = 0;
    this.category = '';

    Object.keys(this).forEach(key => {
      const withName = `with${key.substring(0, 1).toUpperCase()}${key.substring(1)}`;
      this[withName] = value => {
        this[key] = value;
        return this;
      }
    })
  }

  //Calling the builder
  build() {
    const keysNoWithers = Object.keys(this).filter(key => typeof this[key] !== 'function');

    return keysNoWithers.reduce((returnValue, key) => {
      return {
        ...returnValue,
        [key]: this[key]
      }
    }, {})
  }
}

const book = new BookBuilder()
 .withName("The Reckonings")
  .withAuthor('Lacy Johnson')
  .withPrice(31)
  .withCategory('Literature')
  .build();
```

上面的 BookBuilder 类具有与第一个示例相同的效果，但是要短得多，并且当属性越多时，代码的减少就越明显。当调用构造函数时，我们已经用 xxxx 自动创建了所有的构建方法，这里我们使用了一些来自 ES6 的新语法:Object.keys 来获得对象属性的数组，…合并对象的语法。

虽然比第一种方法更难读懂，但是这样做的真正好处是，当我们需要很多构建器类的时候，可以提取上面用 xxx 自动创建的代码，作为父类进行构建。这使得在创建其他构建器类时，很容易创建多个构建器类。

```
//Parent Class
class BaseBuilder {
  init() {
    Object.keys(this).forEach(key => {
      const withName = `with${key.substring(0, 1).toUpperCase()}${key.substring(1)}`;
      this[withName] = value => {
        this[key] = value;
        return this;
      }
    })
  }

  build() {
    const keysNoWithers = Object.keys(this).filter(key => typeof this[key] !== 'function');

    return keysNoWithers.reduce((returnValue, key) => {
      return {
        ...returnValue,
        [key]: this[key]
      }
    }, {})
  }
}

//Subclass 1: BookBuilder
class BookBuilder extends BaseBuilder {
  constructor() {
    super();

    this.name = '';
    this.author = '';
    this.price = 0;
    this.category = '';

    super.init();
  }
}

//Subclass 2
class printHouseBuilder extends BaseBuilder {
  constructor() {
    super();

    this.name = '';
    this.location = '';
    this.quality = '';

    super.init();
  }
}

const book = new BookBuilder()
 .withName("The Reckonings")
  .withAuthor('Lacy Johnson')
  .withPrice(31)
  .withCategory('Literature')
  .build();

const printHouse = new printHouseBuilder()
  .withName('Printers')
  .withLocation('New York')
  .withQuality('A')
  .build();
```

## 摘要

在前面提到的工厂模式中，它们都有一个共同的特征，即对象创建过程是未知的，我们在调用一个函数后返回最终的结果对象。但是在 creator 模式中我们关心对象创建过程，我们通常将创建复杂对象的各种类模块化，而在 ES6 中，我们使用导入和导出的语法来灵活地引用和导出这些模块，以便我们的构造模式最终生成结果对象。

正如您所看到的，构建器模式的使用已经并且只适合于创建极其复杂的对象。在实际的前端业务中，当没有这种极其复杂的对象需要创建时，还是应该直接使用对象字面量或者工厂模式等来创建对象。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***