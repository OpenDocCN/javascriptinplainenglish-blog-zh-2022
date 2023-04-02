# 3 个奇怪的有用的 JavaScript 类技巧

> 原文：<https://javascript.plainenglish.io/3-weird-javascript-class-tricks-that-could-be-useful-c5a78144d574?source=collection_archive---------6----------------------->

![](img/c268adc9f675cba7392efdf0f0216b95.png)

Photo by [Nick Fewings](https://unsplash.com/@jannerboy62?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我喜欢尝试各种东西，JavaScript 有很多奇怪和隐藏的宝石，学习起来总是很有趣。有些只是 API 中的漏洞，有些则是有意或愉快的意外。无论哪种方式，只要有正确的问题和正确的需求，这些都是非常有用的。

## 1 —从构造函数返回对象(单例)

对于一个构造函数来说，返回它所属的类的实例之外的东西是非常奇怪的。在 JavaScript 中，这是可以做到的。

让我们以一个简单的汽车类为例。

```
class **Car** {
  make = '';
  model = '';
  doorsCount = 4;
  wheelsCount = 4;

  **constructor(make, model) {
    this.make = make;
    this.model = model;
  }**
}
```

默认情况下，`new Car(...)`将返回一个类的实例对象，我们可以用它来访问该类的属性和方法。

```
const jeepWrangler = new **Car**('jeep', 'wrangler');jeepWrangler.doorsCount = 2;
jeepWrangler.model; *// wrangler*
```

我们实际上可以从构造函数返回一些东西，例如，一个不同的对象。

```
class **Car** {
  make = '';
  model = '';
  doorsCount = 4;
  wheelsCount = 4;

  **constructor**(make, model) {
    this.make = make;
    this.model = model;

    **return {
      different: true
    }**
  }
}
```

这仅仅意味着当我们实例化类时，我们得到了返回的对象。

```
const jeepWrangler = new **Car**('jeep', 'wrangler');jeepWrangler.model; // undefined
jeepWrangler.**different**; // true
```

但是这只有在你返回一个对象时才有效果。如果你返回一个原语，这个类正常工作。

```
class **Car** {
  make = '';
  model = '';
  doorsCount = 4;
  wheelsCount = 4;

  **constructor**(make, model) {
    this.make = make;
    this.model = model;

    **return 12**
  }
}const jeepWrangler = new Car('jeep', 'wrangler');jeepWrangler.**model**; *// wrangler*
```

那么，你能利用这种古怪做什么呢？

嗯，你可以创建[单例](https://en.wikipedia.org/wiki/Singleton_pattern):一个类，不管你实例化多少次，你总是得到相同的实例。angular[root-provided service](https://angular.io/guide/architecture-services#providing-services)是可以用单例模式完成的一个例子。

```
const **LocalStore** = (() => {
  const data = new Map();
  let **instance** = null;

  return class LocalStore {
    **constructor**() {
      **if(instance === null) {
        instance = this;
      }** **return instance;**
    }
  }
})();const store1 = new **LocalStore**();
const store2 = new **LocalStore**();store1 === store2 // true
```

单例适用于日志、分析、数据库、存储的全局类，也是创建全局变量的替代方法。

你可以用这个技巧来控制类返回的内容。

> [探究本例的**代码**](https://codepen.io/beforesemicolon/pen/bGoxxEM)

## 2-防止类实例化(抽象类)

JavaScript 本身不支持[抽象类](https://en.wikipedia.org/wiki/Abstract_type)的概念，抽象类是一个只能扩展不能实例化的类。然而，有一种不包括装饰者的简单方法可以实现这一点。

```
class **Car** {
  make = '';
  model = '';
  doorsCount = 4;
  wheelsCount = 4;

  constructor(make, model) {
    this.make = make;
    this.model = model;
  }
}class **BMW** extends **Car** { *<- extending Car*
  constructor(model) {
    super('bmw', model);
    this.model = model;
  }
}const bmwM3 = new **Car**('bmw', 'm3'); <- instantiate Car
```

我们可以利用这样一个事实，即我们可以从类构造函数内部访问类构造函数名称。

```
class **Car** {
  make = '';
  model = '';
  doorsCount = 4;
  wheelsCount = 4;

  **constructor**(make, model) {
    this.make = make;
    this.model = model;

    **console.log(this.constructor.name)**
  }
}const bmwM3 = new **Car**('bmw', 'm3');
```

构造函数的名字总是你用来实例化的类，这意味着我们可以用它来了解一个类是被扩展了还是被实例化了。

```
class **Car** {
  make = '';
  model = '';
  doorsCount = 4;
  wheelsCount = 4;

  **constructor**(make, model) {
    this.make = make;
    this.model = model;

    **if(this.constructor.name === 'Car') {
      throw new Error(
        'Car class is abstract. It can only be extended'
      )
    }**
  }
}class BMW **extends Car** {
  constructor(model) {
    super('bmw', model);
    this.model = model;
  }
}const bmwM1 = **new BMW**('m1'); *// works!!*
const bmwM3 = **new Car**('bmw', 'm3'); *// Throws*
```

因此，如果构造函数名与检查它的类相匹配，那么该类将被直接实例化。否则，它将被扩展它的类实例化。

就像那样，你可以创建只能被扩展的类，这对于创建基类来说是完美的。

> [探究本例的**代码**](https://codepen.io/beforesemicolon/pen/rNGZZxX)

## 2 —运行时的多个类扩展(混合)

在 OOP 中，你可以让一个类扩展另一个类，而且你必须在代码执行之前这么做。我在代码中为一些非常具体的问题探索的一件事是在运行时扩展类的想法。

为了向你解释我的意思，我想让你想象你正在玩一个游戏，你有一个`Person`类来代表你的角色。让我们用这样简单的东西。

```
class **Person** {
  #name;
  #dob;

  constructor(name, dob) {
    this.#name = name;
    this.#dob = new Date(dob)
  }

  get **name**() {
    return this.#name;
  }

  get **age**() {
    return (new Date().getFullYear() - this.#dob.getFullYear())
  }
}const johnDoe = new **Person**('John Doe', '09/12/1990');johnDoe.**age**; *// 32*
johnDoe.**name**; *// 'John Doe'*
```

假设在整个游戏中，这个人被 AWS 聘为软件工程师。我们可以使用构造函数来创建一个新的能力。

```
function **Employee**(company, startingDate, title) {
  this.**occupation** = {
    company,
    startingDate: new Date(startingDate),
    title,
  }
  this.**quit** = () => {
    delete this.occupation;
    delete this.quit;
  }
}
```

为了给我们的用户这种能力，我们可以在运行时像这样扩展它:

```
**Employee**.call(**johnDoe**, 'AWS', '02/05/2020', 'software engineer');
```

有了这个，我们现在可以访问`occupation`财产，也可以`quit`工作。

```
johnDoe.**occupation;**
*// {****company****: 'AWS',* ***startingDate****: Wed Feb 05 2020 00:00:00 GMT-0500 (Eastern Standard Time),* ***title****: 'software engineer'}*johnDoe**.quit();**johnDoe**.occupation;** *// undefined*
johnDoe**.quit;** *// undefined*
```

当然，这只是解决这类问题的一种方法，我们也可以尝试插件模式。我想说明的是用多个东西扩展一个类的能力。

这也是实现 mixins 的一种方式，从一个基类开始，在运行时或之前继续扩展它。

在 JavaScript 中引入类之前，这实际上是我们用来扩展类的方式。这个类只是构造函数和原型工作的语法糖。下面也是可以的。类可以扩展构造函数。

```
class **Person** extends **Employee** {
  #name;
  #dob;

  constructor(name, dob, **company, startingDate, title**) {
    **super(company, startingDate, title);**
    this.#name = name;
    this.#dob = new Date(dob)
  }

  get name() {
    return this.#name;
  }

  get age() {
    return (new Date().getFullYear() - this.#dob.getFullYear())
  }

}
```

上面是同样的事情，但是它必须在代码运行之前设置，并且需要`Person`类接受更多的参数。mixin 方式允许您将代码分割成更小的构造函数，这些函数处理包括私有数据在内的所有逻辑。这允许您在代码运行时增加您的类实例。

> [探究本例的**代码**](https://codepen.io/beforesemicolon/pen/KKXxWPr)

## 结论

探索 JavaScript 非常有趣，这意味着取决于你如何改变，你最终会发现一两个有用的技巧。

我曾经认为利用这些东西不好，但是当我进入元编程的世界时，寻找漏洞成为了一种习惯。

我把这些技巧留给你，希望它们有一天会对你有用。

[](https://medium.com/before-semicolon/10-things-to-master-about-javascript-before-you-call-yourself-a-pro-2a5fe237e6ac) [## 在你称自己为专家之前，关于 Javascript 要掌握的 10 件事

### 多年来，Javascript 发生了很大的变化，已经成为最流行的语言之一。它是我的，而且…

medium.com](https://medium.com/before-semicolon/10-things-to-master-about-javascript-before-you-call-yourself-a-pro-2a5fe237e6ac) ![](img/79122679204c8ac0aa65ca22857737ab.png)

***YouTube 频道*** *:* [*前分号*](https://www.youtube.com/channel/UCrU33aw1k9BqTIq2yKXrmBw)***网站****:*[*beforesemicolon.com*](https://beforesemicolon.com/)